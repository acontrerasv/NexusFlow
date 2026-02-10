# NexusFlow Skill Catalog

> Complete documentation of all skills available in the NexusFlow product repository.

## Overview

Skills are specialized capabilities that can be invoked by agents or used directly. They provide domain-specific functionality for common product tasks.

| Category | Count | Primary Use |
|----------|-------|-------------|
| Analysis | 2 | Data analysis, metrics |
| Validation | 2 | PRD and OKR validation |
| Content | 1 | Writing improvement |
| Design | 2 | Design system, branding |
| Strategy | 1 | Strategic frameworks |
| **Total** | **8** | - |

---

## Analysis Skills

### Pipeline Metrics Analyzer

**ID**: `pipeline-metrics-analyzer`

**Purpose**: Analyze sales pipeline metrics, conversion rates, and pipeline health.

**Capabilities**:
- Calculate pipeline conversion rates
- Analyze deal velocity
- Identify pipeline health indicators
- Segment analysis
- Anomaly detection

**When to Use**:
- Analyzing sales data
- Pipeline health reviews
- Forecasting discussions
- Sales team metrics

**Key Outputs**:
| Output | Description |
|--------|-------------|
| Health Score | 0-100 pipeline health rating |
| Stage Analysis | Conversion by stage |
| Velocity Report | Deal speed metrics |
| Recommendations | Improvement suggestions |

**Location**: `.claude/skills/pipeline-metrics-analyzer/SKILL.md`

---

### Business Case Calculator

**ID**: `business-case-calculator`

**Purpose**: Calculate ROI, business impact, and financial projections for initiatives.

**Capabilities**:
- Calculate ROI and NPV
- Model revenue impact
- Project cost savings
- Compare initiative economics
- Generate business cases

**When to Use**:
- Prioritizing features
- Building business cases
- ROI calculations
- Investment decisions

**Key Outputs**:
| Output | Description |
|--------|-------------|
| ROI | Return on investment percentage |
| Payback Period | Months to break even |
| NPV | Net present value |
| Business Case Doc | Full business case document |

**Inputs Needed**:
- Development costs
- Expected benefits (revenue, savings)
- Timeframe

**Location**: `.claude/skills/business-case-calculator/SKILL.md`

---

## Validation Skills

### PRD Compliance Validator

**ID**: `prd-compliance-validator`

**Purpose**: Validate PRD documents against NexusFlow standards.

**Capabilities**:
- Check structure completeness
- Validate required sections
- Assess content quality
- Score PRD compliance (0-100)
- Generate improvement recommendations

**When to Use**:
- Before PRD submission
- PRD reviews
- Quality assurance
- Training new PMs

**Validation Checks**:
| Check | Weight |
|-------|--------|
| Problem Statement | 15% |
| User Stories | 15% |
| Solution | 15% |
| Requirements | 15% |
| Metrics | 15% |
| Timeline | 10% |
| Structure | 10% |
| Risks | 5% |

**Pass Thresholds**:
| Template | Minimum Score |
|----------|--------------|
| Full PRD | 75 |
| OnePage | 70 |
| QuickWin | 65 |

**Location**: `.claude/skills/prd-compliance-validator/SKILL.md`

---

### OKR Alignment Checker

**ID**: `okr-alignment-checker`

**Purpose**: Validate alignment between initiatives and company OKRs.

**Capabilities**:
- Check initiative-OKR alignment
- Score alignment strength
- Identify best-fit OKRs
- Flag misaligned work
- Suggest alignment improvements

**When to Use**:
- PRD validation
- Prioritization discussions
- Strategic planning
- Roadmap reviews

**Alignment Levels**:
| Score | Level | Interpretation |
|-------|-------|----------------|
| 80-100 | Strong | Direct KR impact |
| 60-79 | Good | Clear alignment |
| 40-59 | Moderate | Some connection |
| 20-39 | Weak | Limited alignment |
| 0-19 | None | Not aligned |

**Current OKRs Checked**:
- O1: Reduce enterprise churn
- O2: Accelerate enterprise growth
- O3: Improve product-led growth
- O4: Expand revenue through retention

**Location**: `.claude/skills/okr-alignment-checker/SKILL.md`

---

## Content Skills

### Humanizer

**ID**: `humanizer-skill`

**Purpose**: Improve readability and clarity of written content.

**Capabilities**:
- Improve readability scores
- Simplify complex language
- Fix passive voice
- Remove jargon
- Adapt to audience

**When to Use**:
- Polish PRDs and docs
- Improve user-facing copy
- Make technical content accessible
- Review marketing materials

**Improvements Made**:
| Before | After |
|--------|-------|
| Passive voice | Active voice |
| Jargon | Plain language |
| Long sentences | Shorter sentences |
| Complex words | Simple words |

**Audience Modes**:
- General (8th grade reading level)
- Technical (10th-12th grade)
- Executive (9th-11th grade)

**Location**: `.claude/skills/humanizer-skill/SKILL.md`

---

## Design Skills

### NexusFlow Frontend Design

**ID**: `nexusflow-frontend-design`

**Purpose**: Apply NexusFlow design system to UI components.

**Capabilities**:
- Apply design tokens
- Generate component code
- Ensure accessibility
- Create responsive layouts
- Apply interaction patterns

**Design System Elements**:
| Element | Details |
|---------|---------|
| Colors | Primary blue (#2563EB), semantic colors |
| Typography | Inter font, defined scale |
| Spacing | 4px grid system |
| Components | Buttons, inputs, cards, tables |
| Shadows | 5 elevation levels |

**When to Use**:
- Building UI components
- Reviewing designs
- Creating mockups
- Frontend implementation

**Location**: `.claude/skills/nexusflow-frontend-design/SKILL.md`

---

### NexusFlow Brand Guidelines

**ID**: `nexusflow-brand-guidelines`

**Purpose**: Apply NexusFlow brand standards to materials.

**Capabilities**:
- Logo usage guidance
- Color application
- Typography standards
- Voice and tone
- Visual identity

**Brand Elements**:
| Element | Specification |
|---------|---------------|
| Primary Color | NexusFlow Blue #2563EB |
| Font | Inter |
| Logo | Icon + wordmark |
| Voice | Clear, confident, helpful |

**When to Use**:
- Creating marketing materials
- External communications
- Presentations
- Documentation

**Location**: `.claude/skills/nexusflow-brand-guidelines/SKILL.md`

---

## Strategy Skills

### Product Strategy Stack

**ID**: `product-strategy-stack`

**Purpose**: Provide strategic analysis frameworks for product decisions.

**Capabilities**:
- Apply strategy frameworks
- Conduct market analysis
- Assess opportunities (OST)
- Prioritize with RICE/ICE
- Model market sizing (TAM/SAM/SOM)

**Frameworks Available**:
| Framework | Purpose |
|-----------|---------|
| Opportunity Solution Tree | Map objectives to solutions |
| RICE | Prioritization scoring |
| ICE | Quick prioritization |
| MoSCoW | Scope prioritization |
| Kano | Feature categorization |
| Porter's Five Forces | Market analysis |
| SWOT | Strategic assessment |
| TAM/SAM/SOM | Market sizing |

**When to Use**:
- Strategic planning
- Prioritization sessions
- Market analysis
- Opportunity assessment

**Location**: `.claude/skills/product-strategy-stack/SKILL.md`

---

## Skill Selection Guide

### By Task

| Task | Skill |
|------|-------|
| Analyze pipeline data | pipeline-metrics-analyzer |
| Calculate feature ROI | business-case-calculator |
| Validate PRD | prd-compliance-validator |
| Check OKR alignment | okr-alignment-checker |
| Improve writing | humanizer-skill |
| UI implementation | nexusflow-frontend-design |
| Apply branding | nexusflow-brand-guidelines |
| Strategic analysis | product-strategy-stack |

### By Agent

| Agent | Primary Skills |
|-------|---------------|
| ai-data-analyst | pipeline-metrics-analyzer |
| ai-pm | okr-alignment-checker, product-strategy-stack |
| product-manager | prd-compliance-validator, humanizer-skill |
| ai-frontend-engineer | nexusflow-frontend-design |
| ai-product-marketing | nexusflow-brand-guidelines, humanizer-skill |

---

## Skill Invocation

### From Agents
Agents automatically invoke relevant skills based on context and task.

### Direct Invocation
Skills can be invoked directly:
```
Use the prd-compliance-validator skill to check this PRD
```

### In Commands
Commands like `/prd-writer` invoke skills as part of their workflow.

---

*Last Updated: January 2026*
*See `.claude/skills/[skill-name]/SKILL.md` for full documentation*
