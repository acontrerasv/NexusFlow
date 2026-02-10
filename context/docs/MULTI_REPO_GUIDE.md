# Multi-Repository Guide

> Guide for working across NexusFlow's multiple repositories.

## Repository Overview

NexusFlow's codebase is organized across multiple repositories for modularity and team ownership.

### Repository Map

```
nexusflow/
├── product/              # This repo - Product docs, PRDs, strategy
├── web-app/              # Main web application (Next.js)
├── api-gateway/          # Kong API Gateway config
├── auth-service/         # Authentication service
├── workflow-engine/      # Core workflow execution
├── ai-service/           # AI/ML features
├── integration-service/  # CRM and external integrations
├── notification-service/ # Email, push, in-app notifications
├── analytics-service/    # Usage tracking and reporting
├── billing-service/      # Subscriptions and payments
├── shared-libs/          # Shared TypeScript libraries
├── design-system/        # UI component library
├── infrastructure/       # Terraform and K8s configs
└── docs/                 # Public documentation
```

---

## Repository Details

### Product Repository (`product/`)

**Purpose**: Product documentation, strategy, and AI tools.

**Contents**:
- PRDs and feature specs
- Strategy documents (vision, roadmap, OKRs)
- Data and analytics reports
- AI agents, commands, and skills
- Templates

**Team**: Product, Design

**This is the current repository.**

---

### Web Application (`web-app/`)

**Purpose**: Main NexusFlow web application.

**Stack**: Next.js 14, TypeScript, TailwindCSS, shadcn/ui

**Structure**:
```
web-app/
├── src/
│   ├── app/              # Next.js App Router
│   ├── components/       # React components
│   ├── hooks/            # Custom hooks
│   ├── lib/              # Utilities
│   ├── stores/           # Zustand stores
│   └── types/            # TypeScript types
├── public/               # Static assets
└── tests/                # Test files
```

**Team**: Frontend, Design

**Key Files**:
- `src/app/` - Pages and layouts
- `src/components/ui/` - shadcn/ui components
- `src/lib/api.ts` - API client

---

### API Gateway (`api-gateway/`)

**Purpose**: Request routing, authentication, rate limiting.

**Stack**: Kong 3.4

**Structure**:
```
api-gateway/
├── kong/
│   ├── kong.yml          # Kong declarative config
│   ├── plugins/          # Custom plugins
│   └── scripts/          # Utility scripts
└── terraform/            # Infrastructure
```

**Team**: Platform

---

### Auth Service (`auth-service/`)

**Purpose**: Authentication and authorization.

**Stack**: NestJS 10, PostgreSQL, Redis

**Structure**:
```
auth-service/
├── src/
│   ├── modules/
│   │   ├── auth/         # Authentication logic
│   │   ├── users/        # User management
│   │   ├── sessions/     # Session handling
│   │   └── mfa/          # Multi-factor auth
│   ├── common/           # Shared code
│   └── main.ts           # Entry point
└── test/                 # Tests
```

**Team**: Platform

**Key Endpoints**:
- `POST /auth/login`
- `POST /auth/register`
- `POST /auth/refresh`
- `GET /auth/me`

---

### Workflow Engine (`workflow-engine/`)

**Purpose**: Core workflow execution and management.

**Stack**: NestJS 10, PostgreSQL, RabbitMQ

**Structure**:
```
workflow-engine/
├── src/
│   ├── modules/
│   │   ├── workflows/    # Workflow CRUD
│   │   ├── executions/   # Execution management
│   │   ├── steps/        # Step handlers
│   │   ├── triggers/     # Trigger types
│   │   └── scheduler/    # Scheduled workflows
│   ├── events/           # Event handlers
│   └── main.ts
└── test/
```

**Team**: Engagement

**Key Events**:
- `workflow.created`
- `workflow.execution.started`
- `workflow.execution.completed`

---

### AI Service (`ai-service/`)

**Purpose**: AI/ML features and LLM integration.

**Stack**: Python 3.11, FastAPI, OpenAI, Pinecone

**Structure**:
```
ai-service/
├── app/
│   ├── api/              # FastAPI routes
│   ├── services/
│   │   ├── completion.py # LLM completions
│   │   ├── embedding.py  # Embeddings
│   │   └── rag.py        # RAG pipeline
│   ├── prompts/          # Prompt templates
│   └── main.py
└── tests/
```

**Team**: AI/ML

**Key Endpoints**:
- `POST /ai/complete`
- `POST /ai/embed`
- `POST /ai/suggest/workflow-steps`

---

### Integration Service (`integration-service/`)

**Purpose**: CRM and external system integrations.

**Stack**: NestJS 10, PostgreSQL

**Structure**:
```
integration-service/
├── src/
│   ├── modules/
│   │   ├── salesforce/   # Salesforce integration
│   │   ├── hubspot/      # HubSpot integration
│   │   ├── pipedrive/    # Pipedrive integration
│   │   ├── sync/         # Sync engine
│   │   └── oauth/        # OAuth management
│   └── main.ts
└── test/
```

**Team**: Integration

---

### Design System (`design-system/`)

**Purpose**: Shared UI component library.

**Stack**: React, TypeScript, TailwindCSS, Storybook

**Structure**:
```
design-system/
├── src/
│   ├── components/       # UI components
│   ├── tokens/           # Design tokens
│   └── index.ts          # Exports
├── stories/              # Storybook stories
└── dist/                 # Build output
```

**Team**: Design, Frontend

**Usage**:
```typescript
import { Button, Input, Card } from '@nexusflow/design-system';
```

---

### Infrastructure (`infrastructure/`)

**Purpose**: Infrastructure as code.

**Stack**: Terraform, Kubernetes, ArgoCD

**Structure**:
```
infrastructure/
├── terraform/
│   ├── modules/          # Reusable modules
│   ├── environments/
│   │   ├── dev/
│   │   ├── staging/
│   │   └── production/
│   └── variables.tf
├── kubernetes/
│   ├── base/             # Base manifests
│   └── overlays/         # Environment overlays
└── argocd/               # ArgoCD configs
```

**Team**: Platform

---

## Working Across Repos

### Common Workflows

#### 1. Feature Development

```
1. Product repo: PRD and spec
2. Design system: New components (if needed)
3. Service repo: Backend changes
4. Web app: Frontend changes
5. Infrastructure: Config changes (if needed)
```

#### 2. Bug Fix

```
1. Identify affected repo(s)
2. Fix in relevant service
3. Update tests
4. Deploy
```

#### 3. New Integration

```
1. Integration service: Add connector
2. Web app: Add UI for setup
3. Docs: Update documentation
```

### Cross-Repo Dependencies

| Repo | Depends On |
|------|------------|
| web-app | design-system, shared-libs |
| auth-service | shared-libs |
| workflow-engine | shared-libs, ai-service |
| integration-service | shared-libs |
| ai-service | - |

### Shared Libraries (`shared-libs/`)

Common code shared across services:

```
shared-libs/
├── packages/
│   ├── common/           # Common utilities
│   ├── types/            # Shared TypeScript types
│   ├── errors/           # Error classes
│   ├── logging/          # Logging utilities
│   └── testing/          # Test utilities
```

---

## Development Setup

### Clone All Repos

```bash
# Create workspace
mkdir nexusflow && cd nexusflow

# Clone repos
gh repo clone nexusflow/product
gh repo clone nexusflow/web-app
gh repo clone nexusflow/auth-service
gh repo clone nexusflow/workflow-engine
# ... etc
```

### Local Development

```bash
# Start infrastructure
docker-compose up -d postgres redis rabbitmq

# Start services (in separate terminals)
cd auth-service && npm run start:dev
cd workflow-engine && npm run start:dev
cd web-app && npm run dev
```

### Environment Variables

Each repo has `.env.example`. Copy to `.env` and configure:

```bash
cp .env.example .env
```

---

## Deployment

### Environments

| Environment | URL | Purpose |
|-------------|-----|---------|
| Development | localhost | Local dev |
| Staging | *.staging.nexusflow.io | Testing |
| Production | *.nexusflow.io | Live |

### CI/CD

All repos use GitHub Actions:

1. PR opened → Tests run
2. PR merged to main → Deploy to staging
3. Release tag → Deploy to production

### Release Process

1. Feature branches merged to `main`
2. Create release branch `release/v1.2.3`
3. QA on staging
4. Tag and deploy to production
5. Merge back to `main`

---

## Communication

### Slack Channels

| Channel | Purpose |
|---------|---------|
| #engineering | General engineering |
| #frontend | Web app, design system |
| #backend | Services |
| #platform | Infrastructure |
| #deployments | Deploy notifications |

### Ownership

| Repo | Team | Lead |
|------|------|------|
| product | Product | Alexandra Chen |
| web-app | Frontend | Erik Lindgren |
| auth-service | Platform | Marta Rossi |
| workflow-engine | Engagement | Petra Novak |
| ai-service | AI/ML | Dmitri Volkov |
| integration-service | Integration | Johan Berg |

---

*Last Updated: January 2026*
