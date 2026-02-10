# NexusFlow Services

> Overview of NexusFlow microservices architecture.

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              CLIENTS                                         │
│    Web App    │    Mobile App    │    Public API    │    Webhooks           │
└───────────────┴──────────────────┴──────────────────┴───────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           API GATEWAY (Kong)                                 │
│    Authentication │ Rate Limiting │ Routing │ Load Balancing                │
└─────────────────────────────────────────────────────────────────────────────┘
                                    │
            ┌───────────────────────┼───────────────────────┐
            ▼                       ▼                       ▼
┌───────────────────┐   ┌───────────────────┐   ┌───────────────────┐
│   CORE SERVICE    │   │ WORKFLOW SERVICE  │   │   SYNC SERVICE    │
│                   │   │                   │   │                   │
│ • Organizations   │   │ • Execution       │   │ • CRM Integration │
│ • Users           │   │ • Scheduling      │   │ • Field Mapping   │
│ • Contacts        │   │ • Templates       │   │ • Conflict Res.   │
│ • Plans           │   │                   │   │                   │
└─────────┬─────────┘   └─────────┬─────────┘   └─────────┬─────────┘
          │                       │                       │
          └───────────────────────┼───────────────────────┘
                                  │
                                  ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                         MESSAGE BROKER (RabbitMQ)                            │
│    workflow.* │ sync.* │ notification.* │ analytics.*                        │
└─────────────────────────────────────────────────────────────────────────────┘
                                  │
            ┌───────────────────────────────────────────┐
            ▼                                           ▼
┌───────────────────┐                       ┌───────────────────┐
│   AI SERVICE      │                       │ ANALYTICS SERVICE │
│                   │                       │                   │
│ • Workflow Gen    │                       │ • Event Tracking  │
│ • Suggestions     │                       │ • Metrics         │
│ • Email Compose   │                       │ • Dashboards      │
└───────────────────┘                       └───────────────────┘
                                  │
                                  ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                            DATA LAYER                                        │
│    PostgreSQL (Primary) │ Redis (Cache) │ ClickHouse (Analytics)            │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Service Catalog

| Service | Port | Repository | Owner |
|---------|------|------------|-------|
| API Gateway | 8000 | nexusflow/gateway | Platform |
| Core Service | 3001 | nexusflow/core | Core Team |
| Workflow Service | 3002 | nexusflow/workflow | Engagement |
| Sync Service | 3003 | nexusflow/sync | Integration |
| AI Service | 3004 | nexusflow/ai | AI Team |
| Analytics Service | 3005 | nexusflow/analytics | Data Team |
| Notification Service | 3006 | nexusflow/notify | Platform |

---

## Service Documentation

- [API Gateway](./api-gateway/SERVICE-DOCS.md)
- Core Service (TBD)
- Workflow Service (TBD)
- Sync Service (TBD)
- AI Service (TBD)
- Analytics Service (TBD)

---

## Communication Patterns

### Synchronous (HTTP/gRPC)

Used for real-time operations:
- User authentication
- Data queries
- CRUD operations

```
Client → Gateway → Service → Response
```

### Asynchronous (RabbitMQ)

Used for background processing:
- Workflow execution
- CRM sync
- Email sending
- Analytics events

```
Producer → Queue → Consumer (async)
```

### Event-Driven

Used for cross-service updates:
- contact.created → Sync Service
- workflow.completed → Analytics Service
- subscription.changed → Core Service

---

## Infrastructure

### Kubernetes

All services run on AWS EKS:

```yaml
Namespace: nexusflow-production
Replicas:
  - gateway: 3
  - core: 3
  - workflow: 5
  - sync: 3
  - ai: 2
  - analytics: 2
```

### Databases

| Database | Purpose | Instances |
|----------|---------|-----------|
| PostgreSQL | Primary data | 1 primary + 2 replicas |
| Redis | Caching, sessions | 3-node cluster |
| ClickHouse | Analytics | 2 nodes |
| RabbitMQ | Messaging | 3-node cluster |

### Monitoring

- **Metrics**: Prometheus + Grafana
- **Logging**: ELK Stack
- **Tracing**: Jaeger
- **Alerts**: PagerDuty

---

## Development

### Local Setup

```bash
# Clone all services
git clone git@github.com:nexusflow/services.git
cd services

# Start infrastructure
docker-compose up -d postgres redis rabbitmq

# Start services
npm run dev:all
```

### Service URLs (Local)

| Service | URL |
|---------|-----|
| Gateway | http://localhost:8000 |
| Core | http://localhost:3001 |
| Workflow | http://localhost:3002 |
| Sync | http://localhost:3003 |
| AI | http://localhost:3004 |

---

## Deployment

### Environments

| Environment | URL | Purpose |
|-------------|-----|---------|
| Development | dev.nexusflow.internal | Feature testing |
| Staging | staging.nexusflow.internal | Pre-production |
| Production | api.nexusflow.io | Live |

### CI/CD

```
Push → Build → Test → Deploy (auto for dev/staging)
                   → Deploy (manual for production)
```

---

*Document Owner: Platform Team*
*Last Updated: January 2026*
