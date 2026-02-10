# NexusFlow Service Index

> Complete catalog of NexusFlow platform services and their documentation.

## Service Overview

| Service | Type | Status | Port | Owner |
|---------|------|--------|------|-------|
| API Gateway | Infrastructure | Production | 8000 | Platform |
| Auth Service | Core | Production | 3001 | Platform |
| Workflow Engine | Core | Production | 3002 | Engagement |
| AI Service | Core | Production | 3003 | AI/ML |
| Integration Service | Core | Production | 3004 | Integration |
| Notification Service | Supporting | Production | 3005 | Platform |
| Analytics Service | Supporting | Production | 3006 | Data |
| Billing Service | Core | Production | 3007 | Platform |
| Audit Service | Supporting | Production | 3008 | Platform |
| Scheduler Service | Core | Production | 3009 | Engagement |

---

## Core Services

### API Gateway
- **Type**: Infrastructure
- **Technology**: Kong 3.4
- **Port**: 8000
- **Repository**: `nexusflow/api-gateway`
- **Documentation**: [api-gateway/SERVICE-DOCS.md](../tech/services/api-gateway/SERVICE-DOCS.md)

**Responsibilities**:
- Request routing
- Authentication validation
- Rate limiting
- Request/response transformation
- SSL termination
- Logging and metrics

**Endpoints**:
- `api.nexusflow.io` - Production
- `api.staging.nexusflow.io` - Staging
- `api.dev.nexusflow.io` - Development

---

### Auth Service
- **Type**: Core
- **Technology**: NestJS 10, PostgreSQL
- **Port**: 3001
- **Repository**: `nexusflow/auth-service`

**Responsibilities**:
- User authentication (email/password, OAuth, SAML)
- Token management (JWT)
- Session handling
- MFA management
- API key management
- Permission/role management

**Key Endpoints**:
```
POST /auth/login
POST /auth/register
POST /auth/logout
POST /auth/refresh
POST /auth/forgot-password
POST /auth/reset-password
GET  /auth/me
POST /auth/mfa/enable
POST /auth/mfa/verify
```

**Dependencies**:
- PostgreSQL (auth database)
- Redis (sessions)
- SendGrid (emails)

---

### Workflow Engine
- **Type**: Core
- **Technology**: NestJS 10, PostgreSQL, RabbitMQ
- **Port**: 3002
- **Repository**: `nexusflow/workflow-engine`

**Responsibilities**:
- Workflow CRUD operations
- Workflow execution
- Step orchestration
- Trigger management
- Execution history
- Error handling and retries

**Key Endpoints**:
```
GET    /workflows
POST   /workflows
GET    /workflows/:id
PUT    /workflows/:id
DELETE /workflows/:id
POST   /workflows/:id/run
GET    /workflows/:id/executions
GET    /workflows/:id/executions/:execId
POST   /workflows/:id/pause
POST   /workflows/:id/resume
```

**Events Published**:
- `workflow.created`
- `workflow.updated`
- `workflow.deleted`
- `workflow.execution.started`
- `workflow.execution.completed`
- `workflow.execution.failed`
- `workflow.step.completed`

**Dependencies**:
- PostgreSQL (workflows database)
- RabbitMQ (event bus)
- Integration Service (external actions)
- AI Service (AI steps)

---

### AI Service
- **Type**: Core
- **Technology**: Python 3.11, FastAPI, Pinecone
- **Port**: 3003
- **Repository**: `nexusflow/ai-service`

**Responsibilities**:
- LLM interactions (OpenAI GPT-4)
- Embedding generation
- Vector search
- AI-powered features (suggestions, summaries)
- Prompt management
- Model routing and fallbacks

**Key Endpoints**:
```
POST /ai/complete
POST /ai/embed
POST /ai/search
POST /ai/suggest/workflow-steps
POST /ai/generate/email
POST /ai/analyze/sentiment
GET  /ai/models
```

**Dependencies**:
- OpenAI API
- Anthropic API (fallback)
- Pinecone (vectors)
- Redis (caching)

**Rate Limits**:
- 100 requests/minute per tenant
- 10,000 tokens/request max

---

### Integration Service
- **Type**: Core
- **Technology**: NestJS 10, PostgreSQL
- **Port**: 3004
- **Repository**: `nexusflow/integration-service`

**Responsibilities**:
- CRM integrations (Salesforce, HubSpot, Pipedrive)
- OAuth management for integrations
- Data sync (bi-directional)
- Webhook handling
- Field mapping
- Conflict resolution

**Supported Integrations**:
| Integration | Type | Status | Sync |
|-------------|------|--------|------|
| Salesforce | CRM | GA | Bi-directional |
| HubSpot | CRM | GA | Bi-directional |
| Pipedrive | CRM | GA | Bi-directional |
| Zoho CRM | CRM | Beta | Bi-directional |
| Slack | Communication | GA | One-way |
| Microsoft Teams | Communication | GA | One-way |
| Gmail | Email | GA | Read-only |
| Outlook | Email | GA | Read-only |
| Zapier | Automation | GA | Webhooks |
| Make | Automation | GA | Webhooks |

**Key Endpoints**:
```
GET    /integrations
POST   /integrations/:type/connect
DELETE /integrations/:id/disconnect
POST   /integrations/:id/sync
GET    /integrations/:id/status
POST   /integrations/:id/webhook
GET    /integrations/:id/mappings
PUT    /integrations/:id/mappings
```

**Events Published**:
- `integration.connected`
- `integration.disconnected`
- `integration.sync.started`
- `integration.sync.completed`
- `integration.sync.failed`
- `integration.data.received`

---

### Billing Service
- **Type**: Core
- **Technology**: NestJS 10, PostgreSQL, Stripe
- **Port**: 3007
- **Repository**: `nexusflow/billing-service`

**Responsibilities**:
- Subscription management
- Usage tracking
- Invoice generation
- Payment processing (Stripe)
- Plan management
- Usage-based billing calculations

**Key Endpoints**:
```
GET  /billing/subscription
POST /billing/subscribe
POST /billing/cancel
PUT  /billing/plan
GET  /billing/invoices
GET  /billing/usage
POST /billing/payment-method
GET  /billing/plans
```

**Dependencies**:
- Stripe API
- PostgreSQL
- Analytics Service (usage data)

---

## Supporting Services

### Notification Service
- **Type**: Supporting
- **Technology**: NestJS 10, Redis
- **Port**: 3005
- **Repository**: `nexusflow/notification-service`

**Responsibilities**:
- Email notifications (SendGrid)
- Push notifications
- In-app notifications
- SMS (Twilio)
- Notification preferences
- Template management

**Channels**:
| Channel | Provider | Status |
|---------|----------|--------|
| Email | SendGrid | GA |
| Push (Web) | Firebase | GA |
| Push (Mobile) | Firebase | Beta |
| SMS | Twilio | GA |
| In-app | Native | GA |

---

### Analytics Service
- **Type**: Supporting
- **Technology**: NestJS 10, ClickHouse, PostgreSQL
- **Port**: 3006
- **Repository**: `nexusflow/analytics-service`

**Responsibilities**:
- Event tracking
- Usage metrics
- Dashboard data
- Report generation
- Data export
- Cohort analysis

**Key Metrics Tracked**:
- User activity (logins, sessions)
- Workflow executions
- Feature usage
- API calls
- Integration syncs

---

### Audit Service
- **Type**: Supporting
- **Technology**: NestJS 10, PostgreSQL
- **Port**: 3008
- **Repository**: `nexusflow/audit-service`

**Responsibilities**:
- Audit log storage
- Activity tracking
- Compliance reporting
- Data access logging
- Change tracking

---

### Scheduler Service
- **Type**: Core
- **Technology**: NestJS 10, Redis, BullMQ
- **Port**: 3009
- **Repository**: `nexusflow/scheduler-service`

**Responsibilities**:
- Scheduled workflow triggers
- Recurring task execution
- Cron job management
- Time-based automation
- Timezone handling

---

## Infrastructure

### Databases

| Database | Type | Usage | Location |
|----------|------|-------|----------|
| auth-db | PostgreSQL 16 | Auth Service | AWS RDS |
| workflows-db | PostgreSQL 16 | Workflow Engine | AWS RDS |
| integrations-db | PostgreSQL 16 | Integration Service | AWS RDS |
| billing-db | PostgreSQL 16 | Billing Service | AWS RDS |
| analytics-db | ClickHouse | Analytics Service | AWS EC2 |

### Caching

| Cache | Type | Usage |
|-------|------|-------|
| sessions | Redis 7 | Session storage |
| api-cache | Redis 7 | API response caching |
| rate-limits | Redis 7 | Rate limit counters |
| ai-cache | Redis 7 | AI response caching |

### Message Queue

| Queue | Type | Usage |
|-------|------|-------|
| workflow-events | RabbitMQ | Workflow event bus |
| integration-events | RabbitMQ | Integration events |
| notifications | RabbitMQ | Notification delivery |

---

## API Documentation

- **Production**: https://api.nexusflow.io/docs
- **Staging**: https://api.staging.nexusflow.io/docs
- **OpenAPI Spec**: https://api.nexusflow.io/openapi.json

---

## Health Endpoints

All services expose:
- `GET /health` - Basic health check
- `GET /health/ready` - Readiness probe
- `GET /health/live` - Liveness probe

---

## Monitoring

- **Metrics**: Datadog
- **Logs**: Datadog Log Management
- **Traces**: Datadog APM
- **Alerts**: PagerDuty

---

*Last Updated: January 2026*
