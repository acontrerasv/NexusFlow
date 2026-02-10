# NexusFlow Database Documentation

> Comprehensive database documentation for the NexusFlow platform.

## Overview

NexusFlow uses PostgreSQL as the primary database with additional data stores for specific use cases.

| Database | Purpose | Version |
|----------|---------|---------|
| PostgreSQL | Primary data store | 15.x |
| Redis | Caching, sessions, rate limiting | 7.x |
| ClickHouse | Analytics, event storage | 23.x |

---

## PostgreSQL Configuration

### Instance Configuration

| Parameter | Production | Staging |
|-----------|------------|---------|
| Instance Type | db.r6g.xlarge | db.r6g.large |
| Storage | 500 GB gp3 | 100 GB gp3 |
| IOPS | 12,000 | 3,000 |
| Multi-AZ | Yes | No |
| Read Replicas | 2 | 0 |

### Connection Settings

```
max_connections = 200
shared_buffers = 4GB
effective_cache_size = 12GB
work_mem = 64MB
maintenance_work_mem = 1GB
random_page_cost = 1.1
effective_io_concurrency = 200
```

### Connection Pooling

PgBouncer configuration:

```ini
[databases]
nexusflow = host=postgres.nexusflow.internal port=5432 dbname=nexusflow

[pgbouncer]
pool_mode = transaction
max_client_conn = 1000
default_pool_size = 25
reserve_pool_size = 5
reserve_pool_timeout = 3
```

---

## Schema Overview

### Database Schemas

| Schema | Purpose | Tables |
|--------|---------|--------|
| public | Core business data | 15 |
| workflow | Workflow engine data | 8 |
| analytics | Event and metrics data | 5 |
| audit | Audit logging | 3 |

### Table Summary

| Table | Schema | Rows (Approx) | Growth Rate |
|-------|--------|---------------|-------------|
| organizations | public | 2,000 | 100/month |
| users | public | 16,000 | 800/month |
| contacts | public | 4.5M | 200K/month |
| workflows | workflow | 24,000 | 2K/month |
| workflow_runs | workflow | 15M | 2M/month |
| events | analytics | 50M | 10M/month |

---

## Table Definitions

### Core Tables

#### organizations

```sql
CREATE TABLE public.organizations (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    slug VARCHAR(100) UNIQUE NOT NULL,
    plan_id UUID REFERENCES public.plans(id),
    settings JSONB DEFAULT '{}',
    subscription_status VARCHAR(50) DEFAULT 'active',
    trial_ends_at TIMESTAMP WITH TIME ZONE,
    billing_email VARCHAR(255),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    deleted_at TIMESTAMP WITH TIME ZONE
);

-- Indexes
CREATE INDEX idx_organizations_slug ON public.organizations(slug);
CREATE INDEX idx_organizations_plan ON public.organizations(plan_id);
CREATE INDEX idx_organizations_status ON public.organizations(subscription_status)
    WHERE deleted_at IS NULL;
```

#### users

```sql
CREATE TABLE public.users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    organization_id UUID NOT NULL REFERENCES public.organizations(id),
    email VARCHAR(255) NOT NULL,
    password_hash VARCHAR(255),
    name VARCHAR(255),
    role VARCHAR(50) DEFAULT 'member',
    settings JSONB DEFAULT '{}',
    email_verified_at TIMESTAMP WITH TIME ZONE,
    last_login_at TIMESTAMP WITH TIME ZONE,
    login_count INTEGER DEFAULT 0,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    deleted_at TIMESTAMP WITH TIME ZONE,
    CONSTRAINT uk_users_org_email UNIQUE(organization_id, email)
);

-- Indexes
CREATE INDEX idx_users_organization ON public.users(organization_id)
    WHERE deleted_at IS NULL;
CREATE INDEX idx_users_email ON public.users(email)
    WHERE deleted_at IS NULL;
CREATE INDEX idx_users_role ON public.users(organization_id, role)
    WHERE deleted_at IS NULL;
```

#### contacts

```sql
CREATE TABLE public.contacts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    organization_id UUID NOT NULL REFERENCES public.organizations(id),
    external_id VARCHAR(255),
    email VARCHAR(255),
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    company VARCHAR(255),
    title VARCHAR(255),
    phone VARCHAR(50),
    source VARCHAR(100),
    status VARCHAR(50) DEFAULT 'active',
    score INTEGER DEFAULT 0,
    tags TEXT[],
    custom_fields JSONB DEFAULT '{}',
    last_activity_at TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    deleted_at TIMESTAMP WITH TIME ZONE
);

-- Indexes
CREATE INDEX idx_contacts_organization ON public.contacts(organization_id)
    WHERE deleted_at IS NULL;
CREATE INDEX idx_contacts_email ON public.contacts(organization_id, email)
    WHERE deleted_at IS NULL;
CREATE INDEX idx_contacts_external ON public.contacts(organization_id, external_id)
    WHERE external_id IS NOT NULL AND deleted_at IS NULL;
CREATE INDEX idx_contacts_status ON public.contacts(organization_id, status)
    WHERE deleted_at IS NULL;
CREATE INDEX idx_contacts_tags ON public.contacts USING GIN(tags)
    WHERE deleted_at IS NULL;
CREATE INDEX idx_contacts_custom_fields ON public.contacts USING GIN(custom_fields)
    WHERE deleted_at IS NULL;
```

### Workflow Tables

#### workflows

```sql
CREATE TABLE workflow.workflows (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    organization_id UUID NOT NULL REFERENCES public.organizations(id),
    created_by UUID REFERENCES public.users(id),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    status VARCHAR(50) DEFAULT 'draft',
    trigger_type VARCHAR(50) NOT NULL,
    trigger_config JSONB DEFAULT '{}',
    definition JSONB NOT NULL,
    version INTEGER DEFAULT 1,
    run_count INTEGER DEFAULT 0,
    success_count INTEGER DEFAULT 0,
    failure_count INTEGER DEFAULT 0,
    last_run_at TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    deleted_at TIMESTAMP WITH TIME ZONE
);

-- Indexes
CREATE INDEX idx_workflows_organization ON workflow.workflows(organization_id)
    WHERE deleted_at IS NULL;
CREATE INDEX idx_workflows_status ON workflow.workflows(organization_id, status)
    WHERE deleted_at IS NULL;
CREATE INDEX idx_workflows_trigger ON workflow.workflows(trigger_type)
    WHERE status = 'active' AND deleted_at IS NULL;
```

#### workflow_runs

```sql
CREATE TABLE workflow.workflow_runs (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    workflow_id UUID NOT NULL REFERENCES workflow.workflows(id),
    contact_id UUID REFERENCES public.contacts(id),
    status VARCHAR(50) DEFAULT 'pending',
    trigger_data JSONB,
    context JSONB DEFAULT '{}',
    started_at TIMESTAMP WITH TIME ZONE,
    completed_at TIMESTAMP WITH TIME ZONE,
    error TEXT,
    error_step VARCHAR(100),
    duration_ms INTEGER,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
) PARTITION BY RANGE (created_at);

-- Partitions (created monthly)
CREATE TABLE workflow.workflow_runs_2026_01 PARTITION OF workflow.workflow_runs
    FOR VALUES FROM ('2026-01-01') TO ('2026-02-01');

-- Indexes on partitioned table
CREATE INDEX idx_runs_workflow ON workflow.workflow_runs(workflow_id);
CREATE INDEX idx_runs_contact ON workflow.workflow_runs(contact_id);
CREATE INDEX idx_runs_status ON workflow.workflow_runs(workflow_id, status);
CREATE INDEX idx_runs_created ON workflow.workflow_runs(created_at);
```

---

## Data Types

### Enums

```sql
-- User roles
CREATE TYPE user_role AS ENUM ('owner', 'admin', 'manager', 'member', 'viewer');

-- Workflow status
CREATE TYPE workflow_status AS ENUM ('draft', 'active', 'paused', 'archived');

-- Run status
CREATE TYPE run_status AS ENUM ('pending', 'running', 'completed', 'failed', 'cancelled');

-- Integration provider
CREATE TYPE integration_provider AS ENUM ('salesforce', 'hubspot', 'pipedrive', 'dynamics');
```

### JSONB Schemas

```typescript
// Organization settings
interface OrganizationSettings {
  timezone: string;
  language: string;
  features: {
    ai_enabled: boolean;
    api_access: boolean;
    saml_enabled: boolean;
  };
  branding: {
    logo_url: string;
    primary_color: string;
  };
}

// Workflow definition
interface WorkflowDefinition {
  nodes: Array<{
    id: string;
    type: 'trigger' | 'action' | 'condition' | 'wait';
    config: Record<string, unknown>;
    position: { x: number; y: number };
  }>;
  edges: Array<{
    from: string;
    to: string;
    condition?: string;
  }>;
}

// Contact custom fields
interface ContactCustomFields {
  [key: string]: string | number | boolean | string[];
}
```

---

## Indexing Strategy

### Index Types

| Type | Use Case | Example |
|------|----------|---------|
| B-tree | Equality, range queries | Primary keys, foreign keys |
| GIN | JSONB, arrays | Custom fields, tags |
| GiST | Full-text search | Contact search |
| Partial | Filtered queries | Active records only |

### Index Maintenance

```sql
-- Analyze table statistics (run weekly)
ANALYZE public.contacts;

-- Reindex if bloat > 20% (run monthly)
REINDEX INDEX CONCURRENTLY idx_contacts_organization;

-- Check index usage
SELECT
    schemaname,
    relname,
    indexrelname,
    idx_scan,
    idx_tup_read,
    idx_tup_fetch
FROM pg_stat_user_indexes
WHERE idx_scan < 50
ORDER BY idx_scan;
```

---

## Partitioning

### Partitioned Tables

| Table | Strategy | Partition Key | Retention |
|-------|----------|---------------|-----------|
| workflow_runs | Range (monthly) | created_at | 24 months |
| events | Range (monthly) | timestamp | 12 months |
| sync_logs | Range (monthly) | created_at | 6 months |

### Partition Management

```sql
-- Create new partition (automated via cron)
CREATE TABLE workflow.workflow_runs_2026_02
    PARTITION OF workflow.workflow_runs
    FOR VALUES FROM ('2026-02-01') TO ('2026-03-01');

-- Drop old partition
DROP TABLE workflow.workflow_runs_2024_01;
```

---

## Backup & Recovery

### Backup Schedule

| Type | Frequency | Retention |
|------|-----------|-----------|
| Automated snapshot | Daily | 7 days |
| Point-in-time recovery | Continuous | 7 days |
| Manual snapshot | Weekly | 90 days |
| Cross-region copy | Daily | 30 days |

### Recovery Procedures

```bash
# Restore from snapshot
aws rds restore-db-instance-from-db-snapshot \
    --db-instance-identifier nexusflow-restored \
    --db-snapshot-identifier nexusflow-2026-01-15

# Point-in-time recovery
aws rds restore-db-instance-to-point-in-time \
    --source-db-instance-identifier nexusflow-production \
    --target-db-instance-identifier nexusflow-pitr \
    --restore-time 2026-01-15T10:30:00Z
```

---

## Performance Monitoring

### Key Metrics

| Metric | Warning | Critical |
|--------|---------|----------|
| CPU Utilization | > 70% | > 90% |
| Free Storage | < 50 GB | < 20 GB |
| Read IOPS | > 10,000 | > 12,000 |
| Connection Count | > 150 | > 180 |
| Replication Lag | > 10s | > 60s |

### Query Monitoring

```sql
-- Long-running queries
SELECT
    pid,
    now() - pg_stat_activity.query_start AS duration,
    query,
    state
FROM pg_stat_activity
WHERE (now() - pg_stat_activity.query_start) > interval '5 minutes';

-- Lock monitoring
SELECT
    blocked_locks.pid AS blocked_pid,
    blocking_locks.pid AS blocking_pid,
    blocked_activity.query AS blocked_statement,
    blocking_activity.query AS blocking_statement
FROM pg_catalog.pg_locks blocked_locks
JOIN pg_catalog.pg_stat_activity blocked_activity
    ON blocked_activity.pid = blocked_locks.pid
JOIN pg_catalog.pg_locks blocking_locks
    ON blocking_locks.locktype = blocked_locks.locktype
JOIN pg_catalog.pg_stat_activity blocking_activity
    ON blocking_activity.pid = blocking_locks.pid
WHERE NOT blocked_locks.granted;
```

---

## Security

### Access Control

```sql
-- Application role (limited permissions)
CREATE ROLE nexusflow_app LOGIN PASSWORD 'xxx';
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO nexusflow_app;
GRANT USAGE ON ALL SEQUENCES IN SCHEMA public TO nexusflow_app;

-- Read-only role (for analytics)
CREATE ROLE nexusflow_readonly LOGIN PASSWORD 'xxx';
GRANT SELECT ON ALL TABLES IN SCHEMA public TO nexusflow_readonly;

-- Admin role
CREATE ROLE nexusflow_admin LOGIN PASSWORD 'xxx';
GRANT ALL PRIVILEGES ON DATABASE nexusflow TO nexusflow_admin;
```

### Encryption

- **At Rest**: AES-256 via AWS RDS encryption
- **In Transit**: TLS 1.2+ required
- **Sensitive Columns**: Application-level encryption for credentials

### Row-Level Security

```sql
-- Enable RLS on contacts table
ALTER TABLE public.contacts ENABLE ROW LEVEL SECURITY;

-- Policy: users can only see their organization's contacts
CREATE POLICY contacts_org_isolation ON public.contacts
    FOR ALL
    USING (organization_id = current_setting('app.current_org_id')::uuid);
```

---

## Migration Guidelines

### Migration Process

1. Create migration file with timestamp
2. Test on development
3. Review with team
4. Apply to staging
5. Apply to production (during maintenance window if breaking)

### Example Migration

```sql
-- migrations/20260115_add_contact_score.sql

-- Up
ALTER TABLE public.contacts ADD COLUMN score INTEGER DEFAULT 0;
CREATE INDEX idx_contacts_score ON public.contacts(organization_id, score)
    WHERE deleted_at IS NULL;

-- Down
DROP INDEX idx_contacts_score;
ALTER TABLE public.contacts DROP COLUMN score;
```

---

*Document Owner: Platform Team*
*Last Updated: January 2026*
