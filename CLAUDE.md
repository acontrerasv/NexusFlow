# CLAUDE.md - NexusFlow Product Repository

## What

**NexusFlow** is an AI-powered sales automation platform for B2B teams in EMEA. Series A (Amsterdam, 2023), preparing for Series B in Q4 2026.

This repository contains product documentation, strategy, PRDs, and AI-powered tools. For detailed context, read the relevant file under `context/`.

## Critical Focus Areas

1. **Enterprise Churn** - 12.3% is critical; root cause: integration complexity
2. **Activation** - TTFV 12 days, target <2 days
3. **Enterprise Growth** - Scale from 156 to 312 customers

## Repository Structure

```
.claude/                        # AI configuration
  agents/                       # Agent definitions
  commands/                     # Custom commands
  skills/                       # Specialized skills
context/                        # Business context
  docs/                         # Core docs, conventions, business context
  data/                         # Analytics, churn analysis, metrics
  strategy/                     # Vision, roadmap, OKRs
  prds/                         # Product requirements (by quarter)
  tech/                         # Architecture, services, diagrams
  templates/                    # PRD and document templates
```

## How

```bash
# Regenerate this file after structural changes
/init-safe

# Validate a PRD
/prd-writer
```

No build or deploy steps - this is a documentation repository.

## Key References

| Topic | File |
|-------|------|
| Business overview | `context/docs/BUSINESS_CONTEXT.md` |
| Product vision | `context/strategy/vision/PRODUCT-VISION-2026.md` |
| Current OKRs | `context/strategy/okr/2026/Q2-OKRS.md` |
| Roadmap rationale | `context/strategy/roadmap/INSIGHTS-TO-ROADMAP-Q2-2026.md` |
| Churn deep-dive | `context/data/churn-analysis/CHURN-ANALYSIS-Q1-2026-COMPLETE.md` |
| Usage metrics | `context/data/insights/Q1-2026-PRODUCT-USAGE-SUMMARY.md` |
| Revenue analysis | `context/data/business/REVENUE-METRICS-Q1-2026.md` |
| Naming conventions | `context/docs/CONVENTIONS.md` |
| Tech stack & services | `context/tech/` |
| PRD templates | `context/templates/PRD/GETTING_STARTED.md` |

## AI Agents

| Agent | Use For |
|-------|---------|
| `ai-pm` | General product management |
| `ai-user-researcher` | User research, interviews |
| `ai-data-analyst` | Data analysis, metrics |
| `ai-data-ml-engineer` | AI/ML features, data engineering |
| `ai-product-designer` | Product design, UX strategy |
| `ai-product-marketing` | Positioning, messaging |
| `ai-architect-engineer` | Technical architecture |
| `ai-frontend-engineer` | Frontend development |
| `competitive-benchmarking` | Competitor analysis |
| `nexusflow-architecture-guardian` | Code review, architecture compliance |
| `product-manager` | PRD writing, feature specs |
| `product-usage-analyst` | Usage patterns, user behavior |
| `qa-expert` | Testing strategies, QA |

## Commands

| Command | Description |
|---------|-------------|
| `/init-safe` | Regenerate CLAUDE.md (use instead of `/init`) |
| `/custom-slash-command-writer` | Create new custom commands |
| `/discovery-orchestrator` | Full discovery process |
| `/swarm-orchestrator` | Multi-agent coordination |
| `/prd-writer` | AI-assisted PRD writing |

## Skills

| Skill | Purpose |
|-------|---------|
| `business-case-calculator` | Business case ROI |
| `humanizer-skill` | Content readability improvement |
| `nexusflow-brand-guidelines` | Brand standards, visual identity |
| `nexusflow-frontend-design` | Design system, UI components |
| `okr-alignment-checker` | OKR alignment |
| `pipeline-metrics-analyzer` | Sales pipeline analysis |
| `prd-compliance-validator` | PRD validation |
| `product-strategy-stack` | Strategy frameworks, planning |
