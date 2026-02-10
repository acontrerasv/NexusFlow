# Architecture Rules

> Architectural guidelines and principles for NexusFlow development.

## Overview

These rules ensure consistency, maintainability, and scalability across the NexusFlow platform. All engineers should follow these guidelines when designing and implementing features.

---

## Core Principles

### 1. Domain-Driven Design

Organize code by business domain, not technical layer.

```
✅ Good:
src/
  workflows/
    domain/
    application/
    infrastructure/
  contacts/
    domain/
    application/
    infrastructure/

❌ Bad:
src/
  controllers/
  services/
  repositories/
```

### 2. Dependency Inversion

Depend on abstractions, not implementations.

```typescript
// ✅ Good: Interface in domain, implementation in infrastructure
interface ContactRepository {
  findById(id: string): Promise<Contact>;
}

class PostgresContactRepository implements ContactRepository {
  // implementation
}

// ❌ Bad: Direct dependency on implementation
class ContactService {
  constructor(private db: PgClient) {}
}
```

### 3. Single Responsibility

Each module/class should have one reason to change.

```typescript
// ✅ Good: Separate concerns
class WorkflowExecutor { /* runs workflows */ }
class WorkflowValidator { /* validates definitions */ }
class WorkflowAnalytics { /* tracks metrics */ }

// ❌ Bad: God class
class WorkflowManager {
  execute() {}
  validate() {}
  trackMetrics() {}
  sendNotifications() {}
}
```

---

## Service Architecture

### Service Boundaries

| Service | Responsibility | Database |
|---------|---------------|----------|
| API Gateway | Auth, routing, rate limiting | Redis |
| Core Service | Organizations, users, contacts | PostgreSQL |
| Workflow Engine | Workflow execution | PostgreSQL + Redis |
| Integration Service | CRM sync | PostgreSQL |
| Analytics Service | Events, metrics | ClickHouse |
| AI Service | ML inference | None (stateless) |

### Communication Patterns

| Pattern | Use Case | Example |
|---------|----------|---------|
| Synchronous (HTTP) | Real-time queries | Get contact details |
| Async (RabbitMQ) | Background processing | Workflow execution |
| Events (RabbitMQ) | Cross-service updates | Contact updated |

### Event-Driven Guidelines

```typescript
// Event naming: past tense, domain.entity.action
const events = [
  'workflow.run.started',
  'workflow.run.completed',
  'contact.created',
  'integration.sync.completed'
];

// Event structure
interface DomainEvent {
  id: string;
  type: string;
  timestamp: string;
  organizationId: string;
  payload: Record<string, unknown>;
  metadata: {
    correlationId: string;
    causationId: string;
  };
}
```

---

## API Design

### REST Guidelines

```
# Resource naming
GET    /api/v1/workflows           # List
POST   /api/v1/workflows           # Create
GET    /api/v1/workflows/:id       # Get
PATCH  /api/v1/workflows/:id       # Update
DELETE /api/v1/workflows/:id       # Delete

# Sub-resources
GET    /api/v1/workflows/:id/runs  # List runs for workflow

# Actions (when REST doesn't fit)
POST   /api/v1/workflows/:id/activate
POST   /api/v1/workflows/:id/pause
```

### Response Format

```json
// Success
{
  "data": { ... },
  "meta": {
    "pagination": { ... }
  }
}

// Error
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Human readable message",
    "details": [
      { "field": "email", "message": "Invalid format" }
    ]
  }
}
```

### Versioning

- URL versioning: `/api/v1/`, `/api/v2/`
- Support N-1 versions (current + previous)
- Deprecation notice 6 months before removal

---

## Database Rules

### Schema Design

```sql
-- Always include
- id (UUID, primary key)
- organization_id (for multi-tenancy)
- created_at
- updated_at

-- Soft delete when needed
- deleted_at (nullable timestamp)

-- Example
CREATE TABLE contacts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    organization_id UUID NOT NULL REFERENCES organizations(id),
    email VARCHAR(255) NOT NULL,
    -- ... other fields
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),
    deleted_at TIMESTAMP
);
```

### Query Guidelines

```typescript
// ✅ Good: Always filter by organization
const contacts = await db.query(
  'SELECT * FROM contacts WHERE organization_id = $1 AND deleted_at IS NULL',
  [organizationId]
);

// ❌ Bad: Missing tenant isolation
const contacts = await db.query('SELECT * FROM contacts');
```

### Migration Rules

1. Migrations must be backwards compatible
2. Separate data migrations from schema migrations
3. No dropping columns without deprecation period
4. Always include rollback script

---

## Error Handling

### Error Types

```typescript
// Base error classes
abstract class DomainError extends Error {
  abstract code: string;
  abstract httpStatus: number;
}

class NotFoundError extends DomainError {
  code = 'NOT_FOUND';
  httpStatus = 404;
}

class ValidationError extends DomainError {
  code = 'VALIDATION_ERROR';
  httpStatus = 400;
}

class UnauthorizedError extends DomainError {
  code = 'UNAUTHORIZED';
  httpStatus = 401;
}
```

### Error Logging

```typescript
// Log levels
logger.debug()  // Development only
logger.info()   // Normal operations
logger.warn()   // Recoverable issues
logger.error()  // Errors requiring attention

// Always include context
logger.error('Failed to execute workflow', {
  workflowId,
  organizationId,
  error: err.message,
  stack: err.stack
});
```

---

## Security Rules

### Authentication

- JWT tokens for API authentication
- 15-minute access token expiry
- 7-day refresh token expiry
- SAML SSO for enterprise

### Authorization

```typescript
// Always check permissions
async function updateWorkflow(userId: string, workflowId: string, data: any) {
  const workflow = await workflowRepo.findById(workflowId);

  // Check organization membership
  if (workflow.organizationId !== user.organizationId) {
    throw new UnauthorizedError();
  }

  // Check role permissions
  if (!user.can('workflow:update')) {
    throw new ForbiddenError();
  }

  // Proceed with update
}
```

### Data Protection

- Encrypt sensitive data at rest (credentials, tokens)
- Use parameterized queries (no string concatenation)
- Sanitize all user input
- Log access to sensitive data

---

## Testing Rules

### Test Pyramid

| Level | Coverage | Speed |
|-------|----------|-------|
| Unit | 80%+ | Fast |
| Integration | Key paths | Medium |
| E2E | Critical flows | Slow |

### Test Naming

```typescript
// Format: [Unit]_[Scenario]_[ExpectedResult]
describe('WorkflowExecutor', () => {
  it('should_execute_workflow_when_all_steps_valid', async () => {});
  it('should_fail_when_trigger_conditions_not_met', async () => {});
  it('should_retry_failed_step_up_to_three_times', async () => {});
});
```

### Test Data

```typescript
// Use factories for test data
const workflow = WorkflowFactory.create({
  status: 'active',
  steps: [/* ... */]
});

// Never use production data in tests
```

---

## Performance Rules

### Response Time Targets

| Endpoint Type | Target p95 |
|---------------|------------|
| List endpoints | < 200ms |
| Detail endpoints | < 100ms |
| Create/Update | < 300ms |
| Workflow execution | < 5s |

### Caching Strategy

```typescript
// Cache layers
1. Application cache (in-memory) - 1 minute
2. Redis cache - 5 minutes
3. CDN cache (static assets) - 1 hour

// Cache invalidation
- Invalidate on write
- Use cache-aside pattern
- Include organization_id in cache keys
```

### Query Optimization

```typescript
// ✅ Good: Limit results, use indexes
const contacts = await db.query(`
  SELECT id, email, name
  FROM contacts
  WHERE organization_id = $1
  ORDER BY created_at DESC
  LIMIT 50
`, [orgId]);

// ❌ Bad: Select all, no limit
const contacts = await db.query('SELECT * FROM contacts');
```

---

## Observability

### Logging Standards

```typescript
// Structured logging with correlation
logger.info('Workflow started', {
  workflowId,
  organizationId,
  triggeredBy,
  correlationId: ctx.correlationId
});
```

### Metrics

Key metrics to track:
- Request rate, latency, errors (RED)
- CPU, memory, disk, network (USE)
- Business metrics (workflows run, contacts synced)

### Tracing

- Use OpenTelemetry for distributed tracing
- Propagate trace context across services
- Sample at 10% for production

---

## Documentation

### Code Documentation

```typescript
/**
 * Executes a workflow for a given contact.
 *
 * @param workflowId - The workflow to execute
 * @param contactId - The contact to run workflow for
 * @returns The workflow run record
 * @throws WorkflowNotFoundError if workflow doesn't exist
 * @throws WorkflowInactiveError if workflow is not active
 */
async function executeWorkflow(
  workflowId: string,
  contactId: string
): Promise<WorkflowRun> {
  // ...
}
```

### API Documentation

- OpenAPI spec for all endpoints
- Examples for request/response
- Error scenarios documented

---

*Document Owner: Engineering Team*
*Last Updated: January 2026*
*Review: Quarterly*
