# NexusFlow ERD Documentation

> Complete documentation of the NexusFlow database schema.

## Overview

NexusFlow uses PostgreSQL as the primary database with the following design principles:

- **Multi-tenancy**: All tables include `organization_id` for tenant isolation
- **Soft deletes**: Critical entities use `deleted_at` instead of hard deletes
- **Audit trail**: `created_at`, `updated_at` on all tables
- **JSONB flexibility**: Complex/variable data stored as JSONB

---

## Entity Categories

### Core Entities

Core entities represent the fundamental business objects.

| Entity | Description | Avg Rows/Org |
|--------|-------------|--------------|
| organizations | Customer accounts | 1 |
| users | User accounts within orgs | 8 |
| contacts | Sales contacts/leads | 2,500 |
| plans | Subscription plans | N/A (shared) |

### Workflow Entities

Workflow entities power the automation engine.

| Entity | Description | Avg Rows/Org |
|--------|-------------|--------------|
| workflows | Automation definitions | 12 |
| workflow_runs | Individual executions | 15,000/month |
| workflow_steps | Steps within runs | 75,000/month |
| workflow_templates | Pre-built templates | N/A (shared) |

### Integration Entities

Integration entities manage CRM and external connections.

| Entity | Description | Avg Rows/Org |
|--------|-------------|--------------|
| integrations | Connected services | 2 |
| sync_logs | Sync history | 500/month |
| field_mappings | Custom field maps | 15 |
| sync_conflicts | Unresolved conflicts | 5 |

### Analytics Entities

Analytics entities capture usage and behavior data.

| Entity | Description | Avg Rows/Org |
|--------|-------------|--------------|
| events | User activity events | 50,000/month |
| usage_metrics | Daily usage rollups | 30/month |
| health_scores | Account health data | 1/day |

---

## Detailed Schema

### organizations

Primary tenant entity.

```sql
CREATE TABLE organizations (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    slug VARCHAR(100) UNIQUE NOT NULL,
    plan_id UUID REFERENCES plans(id),
    settings JSONB DEFAULT '{}',
    subscription_status VARCHAR(50) DEFAULT 'active',
    trial_ends_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),
    deleted_at TIMESTAMP
);

CREATE INDEX idx_orgs_slug ON organizations(slug);
CREATE INDEX idx_orgs_plan ON organizations(plan_id);
```

**Settings JSONB Structure**:
```json
{
  "timezone": "Europe/Amsterdam",
  "language": "en",
  "features": {
    "ai_enabled": true,
    "api_access": true
  },
  "branding": {
    "logo_url": "...",
    "primary_color": "#..."
  }
}
```

### users

User accounts with role-based access.

```sql
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    organization_id UUID NOT NULL REFERENCES organizations(id),
    email VARCHAR(255) NOT NULL,
    password_hash VARCHAR(255),
    name VARCHAR(255),
    role VARCHAR(50) DEFAULT 'member',
    settings JSONB DEFAULT '{}',
    email_verified_at TIMESTAMP,
    last_login_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),
    deleted_at TIMESTAMP,
    UNIQUE(organization_id, email)
);

CREATE INDEX idx_users_org ON users(organization_id);
CREATE INDEX idx_users_email ON users(email);
```

**Role Enum Values**:
- `owner` - Full access, billing
- `admin` - Full access, no billing
- `manager` - Team management
- `member` - Standard access
- `viewer` - Read-only

### contacts

Sales contacts/leads.

```sql
CREATE TABLE contacts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    organization_id UUID NOT NULL REFERENCES organizations(id),
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
    last_activity_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),
    deleted_at TIMESTAMP
);

CREATE INDEX idx_contacts_org ON contacts(organization_id);
CREATE INDEX idx_contacts_email ON contacts(organization_id, email);
CREATE INDEX idx_contacts_external ON contacts(organization_id, external_id);
CREATE INDEX idx_contacts_tags ON contacts USING GIN(tags);
```

### workflows

Automation workflow definitions.

```sql
CREATE TABLE workflows (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    organization_id UUID NOT NULL REFERENCES organizations(id),
    created_by UUID REFERENCES users(id),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    status VARCHAR(50) DEFAULT 'draft',
    trigger_type VARCHAR(50) NOT NULL,
    trigger_config JSONB DEFAULT '{}',
    definition JSONB NOT NULL,
    version INTEGER DEFAULT 1,
    run_count INTEGER DEFAULT 0,
    last_run_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),
    deleted_at TIMESTAMP
);

CREATE INDEX idx_workflows_org ON workflows(organization_id);
CREATE INDEX idx_workflows_status ON workflows(organization_id, status);
```

**Status Enum Values**:
- `draft` - Not yet activated
- `active` - Running
- `paused` - Temporarily stopped
- `archived` - No longer in use

**Definition JSONB Structure**:
```json
{
  "nodes": [
    {
      "id": "node_1",
      "type": "trigger",
      "config": {...}
    },
    {
      "id": "node_2",
      "type": "action",
      "action": "send_email",
      "config": {...}
    }
  ],
  "edges": [
    {"from": "node_1", "to": "node_2"}
  ]
}
```

### workflow_runs

Individual workflow executions.

```sql
CREATE TABLE workflow_runs (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    workflow_id UUID NOT NULL REFERENCES workflows(id),
    contact_id UUID REFERENCES contacts(id),
    status VARCHAR(50) DEFAULT 'pending',
    trigger_data JSONB,
    started_at TIMESTAMP,
    completed_at TIMESTAMP,
    error TEXT,
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_runs_workflow ON workflow_runs(workflow_id);
CREATE INDEX idx_runs_contact ON workflow_runs(contact_id);
CREATE INDEX idx_runs_status ON workflow_runs(workflow_id, status);
CREATE INDEX idx_runs_created ON workflow_runs(created_at);
```

**Status Enum Values**:
- `pending` - Queued
- `running` - In progress
- `completed` - Successfully finished
- `failed` - Error occurred
- `cancelled` - Manually stopped

### integrations

External service connections.

```sql
CREATE TABLE integrations (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    organization_id UUID NOT NULL REFERENCES organizations(id),
    provider VARCHAR(50) NOT NULL,
    status VARCHAR(50) DEFAULT 'pending',
    credentials JSONB,  -- encrypted at rest
    field_mapping JSONB DEFAULT '{}',
    sync_config JSONB DEFAULT '{}',
    last_sync_at TIMESTAMP,
    last_error TEXT,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

CREATE UNIQUE INDEX idx_integrations_org_provider
    ON integrations(organization_id, provider);
```

**Provider Enum Values**:
- `salesforce`
- `hubspot`
- `pipedrive`
- `dynamics`

---

## Performance Considerations

### Indexes

Key indexes for common query patterns:

| Table | Index | Purpose |
|-------|-------|---------|
| contacts | org_id, email | Lookup by email |
| workflow_runs | workflow_id, created_at | Recent runs |
| events | org_id, timestamp | Analytics queries |
| sync_logs | integration_id, created_at | Sync history |

### Partitioning

Tables partitioned by time:

| Table | Partition Strategy | Retention |
|-------|-------------------|-----------|
| events | Monthly | 12 months |
| workflow_runs | Monthly | 24 months |
| sync_logs | Monthly | 6 months |

### Connection Pooling

- PgBouncer in transaction mode
- Max 100 connections per service
- Separate pool for analytics queries

---

## Data Retention

| Data Type | Retention | Rationale |
|-----------|-----------|-----------|
| Events | 12 months | Analytics needs |
| Workflow runs | 24 months | Audit trail |
| Sync logs | 6 months | Debugging |
| Contacts | Indefinite | Customer data |
| Soft-deleted | 90 days | Recovery window |

---

## Security

### Encryption

- Credentials encrypted using AES-256
- Encryption keys in AWS KMS
- TLS for all connections

### Access Control

- Row-level security on organization_id
- Read replicas for analytics
- Audit logging on sensitive tables

---

*Document Owner: Platform Team*
*Last Updated: January 2026*
