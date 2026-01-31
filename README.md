# NexusFlow Product Repository

> **Este repositorio es un proyecto DEMO creado por Ariel Contreras, CPO en [Leadsales.io](https://leadsales.io), con el propósito de mostrar cómo utiliza Claude Code en su flujo de trabajo diario.** NexusFlow no es un producto real: es una estructura de referencia que ilustra la forma en que se organiza la documentación de producto, PRDs, estrategia, datos y herramientas de IA dentro de un repositorio. Todos los datos, métricas, nombres y cifras que aparecen son completamente sintéticos. Este estándar de trabajo es el que se aplica en todo el equipo de producto e ingeniería de Leadsales, y sirve como ejemplo práctico de cómo estructurar un repositorio de producto para aprovechar al máximo las capacidades de Claude Code como copiloto de desarrollo y gestión de producto.

> **NexusFlow** - AI-Powered Sales Automation Platform for B2B Teams in EMEA

[![Platform Status](https://img.shields.io/badge/status-production-green)]()
[![Version](https://img.shields.io/badge/version-2.4.1-blue)]()
[![Coverage](https://img.shields.io/badge/coverage-87%25-brightgreen)]()

---

## Overview

This repository contains all product documentation, strategy artifacts, PRDs, technical documentation, and AI-powered tools for the NexusFlow product team.

**NexusFlow** is an AI-powered sales automation platform that helps B2B teams in EMEA automate their sales workflows, integrate with existing CRMs, and leverage AI to optimize their sales pipelines.

### Key Metrics (Q2 2026)

| Metric | Current | Target | Status |
|--------|---------|--------|--------|
| Total Customers | 1,847 | 2,150 | 🟡 On Track |
| Enterprise Customers | 156 | 312 | 🔴 Behind |
| Monthly Churn | 6.8% | 3.5% | 🔴 Critical |
| Enterprise Churn | 12.3% | 2.8% | 🔴 Critical |
| NRR | 108% | 125% | 🟡 On Track |
| DAU | 3,200 | 4,500 | 🟡 On Track |

---

## Repository Structure

```
/
├── README.md                    # This file
├── CLAUDE.md                    # AI assistant instructions
├── .claude/                     # AI configuration
│   ├── settings.json            # Claude Code settings
│   ├── SELECTION_RULES.md       # Agent/skill selection logic
│   ├── COMPONENT_INDEX.md       # Component registry
│   ├── COMPONENT_SCHEMA.md      # Schema definitions
│   ├── agents/                  # AI agent definitions
│   ├── commands/                # Custom slash commands
│   └── skills/                  # Specialized skills
│
└── context/                     # Business context
    ├── docs/                    # Core documentation
    ├── data/                    # Analytics & insights
    ├── strategy/                # Vision, roadmap, OKRs
    ├── prds/                    # Product Requirements Docs
    ├── tech/                    # Technical documentation
    └── templates/               # Document templates
```

---

## Quick Start

### For Product Managers

1. **Understanding the Product**
   - Read [BUSINESS_CONTEXT.md](context/docs/BUSINESS_CONTEXT.md) for company overview
   - Review [PRODUCT-VISION-2026.md](context/strategy/vision/PRODUCT-VISION-2026.md) for strategic direction
   - Check [Q2-OKRS.md](context/strategy/okr/2026/Q2-OKRS.md) for current objectives

2. **Writing PRDs**
   - Start with [GETTING_STARTED.md](context/templates/PRD/GETTING_STARTED.md)
   - Use [00_MASTER_GUIDE.md](context/templates/PRD/00_MASTER_GUIDE.md) for full process
   - Run `/prd-writer` command for AI assistance

3. **Discovery Process**
   - Follow [DISCOVERY_WORKFLOW.md](context/docs/DISCOVERY_WORKFLOW.md)
   - Use `/discovery-orchestrator` for guided discovery

### For Engineers

1. **Architecture Overview**
   - Review [SERVICE_INDEX.md](context/docs/SERVICE_INDEX.md) for service catalog
   - Check [nexusflow-database-documentation.md](context/tech/nexusflow-database-documentation.md) for data model
   - Read [architecture-rules.md](context/tech/rules/architecture-rules.md) for guidelines

2. **Development Standards**
   - Follow [frontend-rules.md](context/tech/rules/frontend-rules.md) for UI development
   - Adhere to [gitflow-rules.md](context/tech/rules/gitflow-rules.md) for version control

### For Data/Analytics

1. **Current Insights**
   - Review [Q1-2026-PRODUCT-USAGE-SUMMARY.md](context/data/insights/Q1-2026-PRODUCT-USAGE-SUMMARY.md)
   - Check [CHURN-ANALYSIS-Q1-2026-COMPLETE.md](context/data/churn-analysis/CHURN-ANALYSIS-Q1-2026-COMPLETE.md)
   - Explore dashboards in `context/data/*/`

---

## AI-Powered Tools

### Available Agents

| Agent | Purpose | Trigger |
|-------|---------|---------|
| `ai-pm` | Product management tasks | Automatic |
| `ai-user-researcher` | User research & interviews | Research tasks |
| `ai-data-analyst` | Data analysis & insights | Analytics queries |
| `ai-product-marketing` | Positioning & messaging | Marketing tasks |
| `ai-architect-engineer` | Technical architecture | Architecture decisions |
| `ai-frontend-engineer` | UI/UX implementation | Frontend work |
| `competitive-benchmarking` | Competitor analysis | Competitive tasks |
| `nexusflow-architecture-guardian` | Architecture compliance | Code reviews |

See [AGENT_CATALOG.md](context/docs/AGENT_CATALOG.md) for complete documentation.

### Available Commands

| Command | Description |
|---------|-------------|
| `/discovery-orchestrator` | Run full discovery process for new features |
| `/swarm-orchestrator` | Coordinate multiple agents for complex tasks |
| `/prd-writer` | AI-assisted PRD writing |
| `/custom-slash-command-writer` | Create new custom commands |

### Available Skills

| Skill | Purpose |
|-------|---------|
| `pipeline-metrics-analyzer` | Analyze sales pipeline metrics |
| `prd-compliance-validator` | Validate PRD completeness |
| `okr-alignment-checker` | Check OKR alignment |
| `business-case-calculator` | Calculate business impact |
| `humanizer-skill` | Improve content readability |
| `nexusflow-frontend-design` | Apply NexusFlow design system |
| `nexusflow-brand-guidelines` | Apply brand standards |
| `product-strategy-stack` | Strategic analysis tools |

See [SKILL_CATALOG.md](context/docs/SKILL_CATALOG.md) for complete documentation.

---

## Product Overview

### What is NexusFlow?

NexusFlow is an AI-powered sales automation platform designed for B2B teams in EMEA. Our platform helps sales teams:

- **Automate Workflows**: Create intelligent automation for repetitive sales tasks
- **Integrate CRMs**: Seamlessly connect with Salesforce, HubSpot, Pipedrive, and more
- **Leverage AI**: Use AI to prioritize leads, predict outcomes, and optimize processes
- **Scale Operations**: Handle enterprise-grade volumes with robust infrastructure

### Target Market

- **Primary**: Mid-market B2B companies (50-500 employees) in EMEA
- **Secondary**: Enterprise companies (500+ employees) seeking automation
- **Vertical Focus**: SaaS, Professional Services, Manufacturing, Financial Services

### Pricing Plans

| Plan | Price | Users | Workflows | Actions/mo |
|------|-------|-------|-----------|------------|
| Starter | €79/mo | 3 | 5 | 10K |
| Professional | €199/mo | 10 | 25 | 100K |
| Enterprise | €499/mo | Unlimited | Unlimited | Unlimited |

See [NEXUSFLOW_PRICING_PLANS.md](context/docs/NEXUSFLOW_PRICING_PLANS.md) for details.

---

## Current Focus (Q2 2026)

### Strategic Priorities

1. **Reduce Enterprise Churn** (Critical)
   - Current: 12.3% → Target: 2.8%
   - Root causes: Integration complexity (28%), Feature gaps (25%)
   - Key initiatives: Smart Onboarding, CRM Sync improvements

2. **Accelerate Enterprise Growth**
   - Current: 156 → Target: 312 customers
   - Focus: Enterprise features, dedicated support, SAML SSO

3. **Improve Activation**
   - Current TTFV: 12 days → Target: <2 days
   - Initiatives: New onboarding flow, AI-guided setup

4. **Expand NRR**
   - Current: 108% → Target: 125%
   - Levers: Usage-based upsells, tier upgrades, add-on modules

### Active Initiatives

| Initiative | Team | Status | Target Date |
|------------|------|--------|-------------|
| User Dashboard Redesign | Activation | Discovery | May 2026 |
| Usage Alerts | Retention | In Progress | April 2026 |
| CRM Sync v2 | Integration | Development | June 2026 |
| AI Workflow Templates | Engagement | Planning | May 2026 |

---

## Tech Stack

### Frontend
- **Framework**: Next.js 14 with App Router
- **Language**: TypeScript 5.3
- **Styling**: TailwindCSS 3.4 + shadcn/ui
- **State**: Zustand + React Query
- **Testing**: Vitest + Playwright

### Backend
- **Runtime**: Node.js 20 LTS
- **Framework**: NestJS 10
- **Database**: PostgreSQL 16 + Redis 7
- **Queue**: RabbitMQ 3.12
- **API**: REST + GraphQL

### AI/ML
- **LLM**: OpenAI GPT-4 Turbo
- **Embeddings**: OpenAI text-embedding-3-large
- **Vector DB**: Pinecone
- **Custom Models**: Fine-tuned classification models

### Infrastructure
- **Cloud**: AWS (EKS, RDS, ElastiCache, SQS)
- **IaC**: Terraform + Terragrunt
- **CI/CD**: GitHub Actions + ArgoCD
- **Monitoring**: Datadog + PagerDuty
- **CDN**: CloudFront

See [SERVICE_INDEX.md](context/docs/SERVICE_INDEX.md) for service documentation.

---

## Key Documents

### Strategy
- [PRODUCT-VISION-2026.md](context/strategy/vision/PRODUCT-VISION-2026.md) - Product vision and strategy
- [ROADMAP-Q2-2026.html](context/strategy/roadmap/ROADMAP-Q2-2026.html) - Interactive roadmap
- [Q2-OKRS.md](context/strategy/okr/2026/Q2-OKRS.md) - Q2 2026 OKRs
- [OPPORTUNITY-SOLUTION-TREE-2026.md](context/strategy/opportunities/OPPORTUNITY-SOLUTION-TREE-2026.md) - OST

### Data & Insights
- [Q1-2026-PRODUCT-USAGE-SUMMARY.md](context/data/insights/Q1-2026-PRODUCT-USAGE-SUMMARY.md) - Usage analytics
- [CHURN-ANALYSIS-Q1-2026-COMPLETE.md](context/data/churn-analysis/CHURN-ANALYSIS-Q1-2026-COMPLETE.md) - Churn deep-dive
- [REVENUE-METRICS-Q1-2026.md](context/data/business/REVENUE-METRICS-Q1-2026.md) - Revenue analysis
- [UX-AUDIT-FINDINGS-Q1-2026.md](context/data/ux/UX-AUDIT-FINDINGS-Q1-2026.md) - UX research

### Technical
- [NEXUSFLOW-ERD-DOCUMENTATION.md](context/tech/diagrams/NEXUSFLOW-ERD-DOCUMENTATION.md) - Database schema
- [architecture-rules.md](context/tech/rules/architecture-rules.md) - Architecture guidelines
- [frontend-rules.md](context/tech/rules/frontend-rules.md) - Frontend standards

---

## Team Structure

### Product Teams

| Team | Focus | PM | Lead |
|------|-------|-----|------|
| Activation | Onboarding & first value | Sofia Martinez | Erik Lindgren |
| Retention | Churn & engagement | Thomas Weber | Anna Kowalski |
| Integration | CRM & external systems | Marie Dubois | Johan Berg |
| Engagement | Core workflow features | Klaus Schmidt | Petra Novak |
| Platform | Infrastructure & APIs | Henrik Olsen | Marta Rossi |

### Key Contacts

- **CPO**: Alexandra Chen (alexandra@nexusflow.io)
- **VP Engineering**: Marcus Weber (marcus@nexusflow.io)
- **VP Design**: Ingrid Svensson (ingrid@nexusflow.io)
- **Head of Data**: Dmitri Volkov (dmitri@nexusflow.io)

---

## Contributing

### For PRDs

1. Clone the repository
2. Create a branch: `feature/prd-[feature-name]`
3. Use templates from `context/templates/PRD/`
4. Submit PR for review

### For Documentation

1. Follow existing conventions
2. Update `SERVICE_INDEX.md` for new services
3. Keep metrics current
4. Cross-reference related documents

### For AI Components

1. Follow patterns in existing agents/skills
2. Test with sample scenarios
3. Document in appropriate catalog
4. Update `COMPONENT_INDEX.md`

---

## Changelog

### 2026-Q2

- Added Usage Alerts feature spec
- Updated churn analysis with Q1 data
- New AI Workflow Templates initiative
- Dashboard redesign discovery started

### 2026-Q1

- Launched CRM Sync v1.5
- Completed Smart Onboarding MVP
- Updated pricing plans
- New enterprise features

### 2025-Q4

- Initial repository structure
- Core agent definitions
- Template system v1
- PRD workflow established

---

## Support

- **Internal Wiki**: https://wiki.nexusflow.io
- **Slack**: #product-team, #engineering
- **Email**: product@nexusflow.io

---

*Last updated: January 2026*
*Maintained by: NexusFlow Product Team*
