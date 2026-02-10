# Agent & Skill Selection Rules

This document defines the rules for automatically selecting agents and skills based on user intent and context.

## Agent Selection Matrix

### Primary Intent Detection

| User Intent | Primary Agent | Secondary Agent | Confidence |
|-------------|--------------|-----------------|------------|
| PRD writing, feature specs | `product-manager` | `ai-pm` | High |
| User research, interviews | `ai-user-researcher` | - | High |
| Data analysis, metrics | `ai-data-analyst` | `product-usage-analyst` | High |
| Marketing, positioning | `ai-product-marketing` | - | High |
| Architecture, system design | `ai-architect-engineer` | - | High |
| Frontend, UI/UX code | `ai-frontend-engineer` | - | High |
| ML/AI features | `ai-data-ml-engineer` | - | High |
| Design, visual | `ai-product-designer` | - | High |
| Competitor analysis | `competitive-benchmarking` | - | High |
| Code review, standards | `nexusflow-architecture-guardian` | - | High |
| QA, testing | `qa-expert` | - | High |

### Keyword-Based Selection

```yaml
product-manager:
  keywords:
    - prd
    - requirements
    - feature
    - roadmap
    - prioritization
    - user story
    - acceptance criteria
  file_patterns:
    - "context/prds/**/*.md"
    - "context/templates/PRD/**"

ai-user-researcher:
  keywords:
    - user research
    - interview
    - persona
    - user needs
    - pain points
    - customer feedback
    - usability
  file_patterns:
    - "context/data/ux/**"

ai-data-analyst:
  keywords:
    - metrics
    - analytics
    - dashboard
    - churn
    - retention
    - cohort
    - funnel
    - conversion
  file_patterns:
    - "context/data/**/*.csv"
    - "context/data/**/*.md"
    - "**/*dashboard*.html"

ai-product-marketing:
  keywords:
    - positioning
    - messaging
    - value proposition
    - competitive
    - market
    - launch
    - go-to-market
  file_patterns:
    - "context/docs/BUSINESS_CONTEXT.md"

ai-architect-engineer:
  keywords:
    - architecture
    - system design
    - microservices
    - api
    - database
    - infrastructure
    - scalability
  file_patterns:
    - "context/tech/**"

ai-frontend-engineer:
  keywords:
    - frontend
    - react
    - nextjs
    - component
    - ui
    - styling
    - tailwind
  file_patterns:
    - "**/*.tsx"
    - "**/*.css"

competitive-benchmarking:
  keywords:
    - competitor
    - benchmark
    - market analysis
    - alternative
    - comparison
  file_patterns: []

nexusflow-architecture-guardian:
  keywords:
    - code review
    - architecture review
    - standards
    - compliance
    - best practices
  file_patterns:
    - "context/tech/rules/**"
```

### Context-Based Selection

```yaml
context_rules:
  - condition: "file in context/prds/"
    agent: product-manager
    reason: "Working on PRD files"

  - condition: "file in context/data/churn-analysis/"
    agent: ai-data-analyst
    reason: "Analyzing churn data"

  - condition: "file in context/data/insights/"
    agent: product-usage-analyst
    reason: "Product usage analysis"

  - condition: "file in context/tech/"
    agent: ai-architect-engineer
    reason: "Technical documentation"

  - condition: "file extension is .tsx or .css"
    agent: ai-frontend-engineer
    reason: "Frontend code"

  - condition: "file in context/strategy/"
    agent: ai-pm
    reason: "Strategic planning"
```

## Skill Selection Rules

### Automatic Skill Loading

| Trigger | Skill | Condition |
|---------|-------|-----------|
| PRD validation | `prd-compliance-validator` | When reviewing PRDs |
| OKR discussion | `okr-alignment-checker` | When discussing OKRs or strategy |
| Business case | `business-case-calculator` | When calculating ROI or impact |
| Pipeline analysis | `pipeline-metrics-analyzer` | When analyzing sales metrics |
| Content writing | `humanizer-skill` | When polishing documentation |
| Frontend design | `nexusflow-frontend-design` | When creating UI components |
| Branding | `nexusflow-brand-guidelines` | When applying brand standards |
| Strategy | `product-strategy-stack` | When doing strategic analysis |

### Skill Keyword Triggers

```yaml
pipeline-metrics-analyzer:
  triggers:
    - "pipeline"
    - "sales metrics"
    - "conversion rate"
    - "deal velocity"

prd-compliance-validator:
  triggers:
    - "validate prd"
    - "check prd"
    - "prd review"
    - "requirements complete"

okr-alignment-checker:
  triggers:
    - "okr"
    - "objective"
    - "key result"
    - "alignment"

business-case-calculator:
  triggers:
    - "business case"
    - "roi"
    - "impact"
    - "cost-benefit"
    - "revenue impact"

humanizer-skill:
  triggers:
    - "humanize"
    - "improve writing"
    - "make readable"
    - "polish"

nexusflow-frontend-design:
  triggers:
    - "design system"
    - "component"
    - "ui pattern"
    - "nexusflow style"

nexusflow-brand-guidelines:
  triggers:
    - "brand"
    - "logo"
    - "colors"
    - "typography"
    - "visual identity"

product-strategy-stack:
  triggers:
    - "strategy"
    - "vision"
    - "north star"
    - "opportunity"
    - "market analysis"
```

## Command Selection

### Command Intent Mapping

| User Request | Command | Confidence |
|--------------|---------|------------|
| "Run discovery" | `/discovery-orchestrator` | High |
| "Write a PRD" | `/prd-writer` | High |
| "Coordinate agents" | `/swarm-orchestrator` | Medium |
| "Create command" | `/custom-slash-command-writer` | High |

## Selection Priority

1. **Explicit Request**: User explicitly names agent/skill
2. **Command Trigger**: User invokes a slash command
3. **File Context**: Based on files being edited
4. **Keyword Match**: Based on keywords in request
5. **Default**: Falls back to `ai-pm`

## Multi-Agent Scenarios

### Discovery Process
- Primary: `ai-user-researcher`
- Support: `ai-data-analyst`, `product-manager`
- Orchestrator: `/discovery-orchestrator`

### PRD Creation
- Primary: `product-manager`
- Support: `ai-architect-engineer`, `ai-product-designer`
- Validator: `prd-compliance-validator`

### Technical Specification
- Primary: `ai-architect-engineer`
- Support: `ai-frontend-engineer`, `ai-data-ml-engineer`
- Guardian: `nexusflow-architecture-guardian`

## Override Rules

Users can override automatic selection by:
1. Explicitly naming an agent: "Ask the data analyst..."
2. Using @ mentions: "@ai-data-analyst"
3. Specifying in command: `/discovery-orchestrator --agent=ai-user-researcher`

## Confidence Thresholds

| Confidence | Action |
|------------|--------|
| High (>0.8) | Auto-select agent |
| Medium (0.5-0.8) | Suggest agent, ask for confirmation |
| Low (<0.5) | Use default agent, offer alternatives |
