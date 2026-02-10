# Agent Workflows

> Standard workflows combining multiple agents for common tasks.

## Overview

This document defines standard workflows that coordinate multiple agents to accomplish complex tasks. Each workflow specifies the sequence of agents, their interactions, and expected outputs.

---

## Workflow 1: Feature Discovery

**Purpose**: Comprehensive discovery process for new features.

**Trigger**: `/discovery-orchestrator`

**Duration**: 45-90 minutes

### Flow

```
┌──────────────────┐
│    START         │
│  Feature Idea    │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│   ai-pm          │  Phase 1: Context (5 min)
│   Gather context │  - Existing docs
│   Map to OKRs    │  - Strategic alignment
└────────┬─────────┘
         │
    ┌────┴────┐
    ▼         ▼
┌───────┐ ┌───────────────────┐
│ ai-   │ │ competitive-      │  Phase 2: Research (15 min)
│ data- │ │ benchmarking      │  - Parallel execution
│analyst│ │                   │
└───┬───┘ └─────────┬─────────┘
    │               │
    └───────┬───────┘
            ▼
┌──────────────────┐
│ ai-user-         │  Phase 3: User Insights (15 min)
│ researcher       │  - Review research
│                  │  - Map pain points
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ product-manager  │  Phase 4: Synthesis (10 min)
│ Synthesize       │  - Create summary
│ Create summary   │  - Recommendations
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│    OUTPUT        │
│ DISCOVERY_       │
│ SUMMARY.md       │
└──────────────────┘
```

### Outputs

- `DISCOVERY_SUMMARY.md` - Comprehensive discovery document
- Problem hypothesis
- User insights
- Data evidence
- Competitive context
- Recommended next steps

---

## Workflow 2: PRD Creation

**Purpose**: Create complete PRD documentation.

**Trigger**: `/prd-writer`

**Duration**: 30-60 minutes

### Flow

```
┌──────────────────┐
│    START         │
│  Feature Brief   │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ product-manager  │  Phase 1: Problem Definition
│ Problem Brief    │  - Problem statement
│                  │  - Evidence
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ product-manager  │  Phase 2: JTBD Analysis
│ JTBD Framework   │  - Jobs to be done
│                  │  - User needs
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ product-manager  │  Phase 3: Solution Design
│ + ai-architect-  │  - Solution hypothesis
│   engineer       │  - Technical feasibility
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ product-manager  │  Phase 4: Full PRD
│ Requirements     │  - User stories
│                  │  - Acceptance criteria
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ prd-compliance-  │  Phase 5: Validation
│ validator        │  - Completeness check
│ okr-alignment-   │  - OKR alignment
│ checker          │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│    OUTPUT        │
│ Full PRD Suite   │
│ (5 documents)    │
└──────────────────┘
```

### Outputs

- `00_FEATURE_BRIEF.md`
- `01_Problem_Brief.md`
- `02_JTBD.md`
- `03_Solution_Hypothesis.md`
- `04_PRD.md`

---

## Workflow 3: Data-Driven Analysis

**Purpose**: Comprehensive data analysis for decision making.

**Trigger**: Manual - request analysis

**Duration**: 20-40 minutes

### Flow

```
┌──────────────────┐
│    START         │
│  Analysis Need   │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ ai-data-analyst  │  Phase 1: Data Gathering
│ Gather metrics   │  - Pull relevant data
│                  │  - Identify sources
└────────┬─────────┘
         │
    ┌────┴────┐
    ▼         ▼
┌───────┐ ┌───────────────────┐
│ ai-   │ │ product-usage-    │  Phase 2: Analysis
│ data- │ │ analyst           │  - Parallel deep-dives
│analyst│ │                   │  - Different angles
└───┬───┘ └─────────┬─────────┘
    │               │
    └───────┬───────┘
            ▼
┌──────────────────┐
│ pipeline-metrics-│  Phase 3: Specialized Analysis
│ analyzer (skill) │  - Apply domain expertise
│                  │  - Calculate metrics
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ ai-data-analyst  │  Phase 4: Synthesis
│ Create report    │  - Insights
│ Build dashboard  │  - Recommendations
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│    OUTPUT        │
│ Analysis Report  │
│ Dashboard (HTML) │
└──────────────────┘
```

### Outputs

- Analysis report (Markdown)
- Interactive dashboard (HTML)
- Key insights
- Recommendations

---

## Workflow 4: Technical Specification

**Purpose**: Create technical specifications for features.

**Trigger**: After PRD approval

**Duration**: 30-45 minutes

### Flow

```
┌──────────────────┐
│    START         │
│  Approved PRD    │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ ai-architect-    │  Phase 1: Architecture
│ engineer         │  - System design
│                  │  - Service changes
└────────┬─────────┘
         │
    ┌────┴────────────┐
    ▼                 ▼
┌───────────┐ ┌──────────────┐
│ ai-       │ │ ai-data-ml-  │  Phase 2: Specialists
│ frontend- │ │ engineer     │  - UI specs
│ engineer  │ │              │  - AI components
└─────┬─────┘ └──────┬───────┘
      │              │
      └──────┬───────┘
             ▼
┌──────────────────┐
│ qa-expert        │  Phase 3: Test Strategy
│ Test plan        │  - Test cases
│                  │  - Coverage requirements
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ nexusflow-       │  Phase 4: Review
│ architecture-    │  - Standards compliance
│ guardian         │  - Best practices
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│    OUTPUT        │
│ Tech Spec Doc    │
│ Test Plan        │
└──────────────────┘
```

### Outputs

- Technical specification document
- API design
- Database changes
- Test plan
- Architecture decision records

---

## Workflow 5: Competitive Analysis

**Purpose**: Comprehensive competitive intelligence.

**Trigger**: Manual - competitive request

**Duration**: 30-45 minutes

### Flow

```
┌──────────────────┐
│    START         │
│  Competitor(s)   │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ competitive-     │  Phase 1: Research
│ benchmarking     │  - Feature comparison
│                  │  - Pricing analysis
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ ai-product-      │  Phase 2: Positioning
│ marketing        │  - Differentiation
│                  │  - Messaging
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ competitive-     │  Phase 3: Battle Card
│ benchmarking     │  - Why we win
│                  │  - Objection handling
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│    OUTPUT        │
│ Battle Card      │
│ Competitive Brief│
└──────────────────┘
```

### Outputs

- Competitive analysis document
- Battle card
- Feature comparison matrix
- Positioning recommendations

---

## Workflow 6: Launch Planning

**Purpose**: Plan and document feature launches.

**Trigger**: Feature approaching release

**Duration**: 20-30 minutes

### Flow

```
┌──────────────────┐
│    START         │
│  Feature Ready   │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ product-manager  │  Phase 1: Launch Brief
│ Document feature │  - What's launching
│                  │  - Target users
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ ai-product-      │  Phase 2: Messaging
│ marketing        │  - Value props
│                  │  - Copy
└────────┬─────────┘
         │
    ┌────┴────┐
    ▼         ▼
┌───────┐ ┌───────────────────┐
│ ai-   │ │ qa-expert         │  Phase 3: Readiness
│ pm    │ │                   │  - Checklist
└───┬───┘ └─────────┬─────────┘  - Testing
    │               │
    └───────┬───────┘
            ▼
┌──────────────────┐
│    OUTPUT        │
│ Launch Plan      │
│ Checklist        │
└──────────────────┘
```

### Outputs

- Launch plan document
- Marketing assets
- Launch checklist
- Metrics to track

---

## Workflow Orchestration

### Parallel Execution

When agents can work independently, they execute in parallel to reduce total time.

```
Sequential: A → B → C → D = 40 min
Parallel:   A → [B,C] → D = 25 min
```

### Error Handling

| Scenario | Action |
|----------|--------|
| Agent timeout | Continue with partial results |
| Missing data | Flag gap, proceed |
| Conflicting outputs | Present both, recommend |

### Handoff Protocol

Each agent handoff includes:
1. Summary of work completed
2. Key findings
3. Open questions
4. Recommended next steps

---

## Custom Workflows

To create custom workflows, use `/swarm-orchestrator` with specific agents and parameters.

Example:
```
/swarm-orchestrator
  task="Quarterly product review"
  agents=["ai-data-analyst", "ai-pm", "product-usage-analyst"]
  mode=parallel
```

---

*Last Updated: January 2026*
*See `/discovery-orchestrator` and `/swarm-orchestrator` for implementation*
