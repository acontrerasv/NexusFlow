---
name: product-strategy-stack
description: Provides strategic analysis frameworks, planning tools, and strategy methodologies for product decisions. Includes market analysis, opportunity assessment, and strategic planning capabilities.
---

# Product Strategy Stack

## Capabilities

- Apply strategy frameworks (Porter's, SWOT, etc.)
- Conduct market analysis
- Assess opportunities using OST
- Prioritize using various frameworks
- Create strategic narratives
- Analyze competitive positioning
- Model market sizing (TAM/SAM/SOM)

## Strategic Frameworks

### 1. Opportunity Solution Tree (OST)

```
                    ┌─────────────────┐
                    │   OBJECTIVE     │
                    │ (Desired Outcome)│
                    └────────┬────────┘
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
┌───────▼───────┐   ┌───────▼───────┐   ┌───────▼───────┐
│ OPPORTUNITY 1 │   │ OPPORTUNITY 2 │   │ OPPORTUNITY 3 │
└───────┬───────┘   └───────┬───────┘   └───────────────┘
        │                   │
   ┌────┴────┐         ┌────┴────┐
   │         │         │         │
┌──▼──┐   ┌──▼──┐   ┌──▼──┐   ┌──▼──┐
│Sol A│   │Sol B│   │Sol C│   │Sol D│
└─────┘   └─────┘   └─────┘   └─────┘
```

### 2. RICE Prioritization

```python
def calculate_rice(reach, impact, confidence, effort):
    """
    RICE Score = (Reach × Impact × Confidence) / Effort

    - Reach: Number of users affected per quarter
    - Impact: 0.25 (minimal) to 3 (massive)
    - Confidence: 0-100%
    - Effort: Person-months
    """
    return (reach * impact * confidence) / effort
```

| Impact Level | Score | Description |
|--------------|-------|-------------|
| Massive | 3.0 | Fundamentally changes user behavior |
| High | 2.0 | Significant improvement |
| Medium | 1.0 | Noticeable improvement |
| Low | 0.5 | Minor improvement |
| Minimal | 0.25 | Barely noticeable |

### 3. ICE Scoring

```python
def calculate_ice(impact, confidence, ease):
    """
    ICE Score = (Impact + Confidence + Ease) / 3

    All scores 1-10
    """
    return (impact + confidence + ease) / 3
```

### 4. MoSCoW Method

| Priority | Meaning | Guideline |
|----------|---------|-----------|
| Must Have | Critical requirements | 60% of effort |
| Should Have | Important, not vital | 20% of effort |
| Could Have | Nice to have | 20% of effort |
| Won't Have | Out of scope | 0% this release |

### 5. Kano Model

```
           Satisfaction ↑
                 │
    Delighters   │   ●
         ●       │     ●
                 │       ●
─────────────────┼─────────────────→ Fulfillment
        ●        │         Performance
       ●         │        ●
      ●  Basic   │       ●
                 │
```

| Category | Description | Example |
|----------|-------------|---------|
| Must-be | Expected, causes dissatisfaction if missing | Login works |
| Performance | More is better, linear satisfaction | Faster sync |
| Delighters | Unexpected, creates delight | AI suggestions |
| Indifferent | No impact on satisfaction | Backend choice |
| Reverse | Causes dissatisfaction when present | Forced tutorials |

## Market Analysis

### TAM/SAM/SOM Model

```
┌─────────────────────────────────────────┐
│                  TAM                     │
│    Total Addressable Market              │
│    (All potential revenue)               │
│    ┌─────────────────────────────────┐  │
│    │              SAM                 │  │
│    │   Serviceable Addressable Market │  │
│    │   (Your target segment)          │  │
│    │   ┌─────────────────────────┐   │  │
│    │   │          SOM            │   │  │
│    │   │  Serviceable Obtainable │   │  │
│    │   │  (Realistic capture)    │   │  │
│    │   └─────────────────────────┘   │  │
│    └─────────────────────────────────┘  │
└─────────────────────────────────────────┘
```

### NexusFlow Market Sizing

| Market | Size | Calculation |
|--------|------|-------------|
| TAM | €8.5B | Global sales automation software |
| SAM | €2.1B | EMEA B2B sales automation |
| SOM | €85M | Mid-market EMEA (5% capture) |

### Porter's Five Forces

```
                    ┌─────────────────────┐
                    │   New Entrants      │
                    │   (Threat: Medium)  │
                    └──────────┬──────────┘
                               │
                               ▼
┌─────────────┐    ┌─────────────────────┐    ┌─────────────┐
│  Suppliers  │───▶│     Industry        │◀───│   Buyers    │
│  (Low)      │    │    Rivalry          │    │   (Medium)  │
└─────────────┘    │    (High)           │    └─────────────┘
                   └──────────┬──────────┘
                              │
                              ▼
                   ┌─────────────────────┐
                   │   Substitutes       │
                   │   (Medium)          │
                   └─────────────────────┘
```

### SWOT Analysis Template

```markdown
| Strengths | Weaknesses |
|-----------|------------|
| • AI-first platform | • Limited enterprise features |
| • Strong EMEA presence | • Smaller integration library |
| • Fast implementation | • Brand awareness |

| Opportunities | Threats |
|---------------|---------|
| • Enterprise expansion | • Well-funded competitors |
| • AI feature demand | • Market consolidation |
| • GDPR compliance advantage | • Economic slowdown |
```

## Strategic Planning

### Vision-Strategy-Execution Cascade

```
┌─────────────────────────────────────────┐
│                VISION                    │
│    Where we want to be (3-5 years)      │
└─────────────────────┬───────────────────┘
                      │
┌─────────────────────▼───────────────────┐
│               STRATEGY                   │
│    How we'll get there (1-3 years)      │
└─────────────────────┬───────────────────┘
                      │
┌─────────────────────▼───────────────────┐
│                 OKRs                     │
│    Measurable goals (Quarterly)         │
└─────────────────────┬───────────────────┘
                      │
┌─────────────────────▼───────────────────┐
│              INITIATIVES                 │
│    Projects and features (Weekly)        │
└─────────────────────────────────────────┘
```

### Strategy Canvas

| Factor | NexusFlow | Competitor A | Competitor B |
|--------|-----------|--------------|--------------|
| Price | ●●●○○ | ●●○○○ | ●●●●○ |
| AI Features | ●●●●● | ●●●○○ | ●●○○○ |
| Integrations | ●●●○○ | ●●●●● | ●●●○○ |
| Ease of Use | ●●●●○ | ●●○○○ | ●●●●● |
| Enterprise | ●●○○○ | ●●●●● | ●●●○○ |
| Support | ●●●●○ | ●●●○○ | ●●○○○ |

### Value Proposition Canvas

```
┌──────────────────────────────────────────────────────────┐
│                    CUSTOMER PROFILE                       │
├─────────────────┬───────────────────┬────────────────────┤
│    Jobs         │     Pains         │      Gains         │
│  • Close deals  │  • Manual entry   │  • More revenue    │
│  • Track leads  │  • Tool sprawl    │  • Less admin      │
│  • Report to    │  • No visibility  │  • Better insights │
│    leadership   │                   │                    │
└─────────────────┴───────────────────┴────────────────────┘
                           │
                           ▼
┌──────────────────────────────────────────────────────────┐
│                    VALUE PROPOSITION                      │
├─────────────────┬───────────────────┬────────────────────┤
│   Products &    │  Pain Relievers   │   Gain Creators    │
│   Services      │                   │                    │
│  • Workflows    │  • Auto sync CRM  │  • AI suggestions  │
│  • AI Assist    │  • One platform   │  • Real-time dash  │
│  • Dashboards   │  • Easy setup     │  • Predictive      │
└─────────────────┴───────────────────┴────────────────────┘
```

## Output Templates

### Strategic Analysis Report

```markdown
# Strategic Analysis: [Topic]

## Executive Summary
[2-3 paragraph overview]

## Market Context
### Market Size
| Segment | Size | Growth |
|---------|------|--------|

### Competitive Landscape
[Analysis]

## Strategic Assessment
### SWOT
[4-quadrant analysis]

### Key Insights
1. [Insight 1]
2. [Insight 2]

## Opportunity Assessment
### Opportunities Identified
| Opportunity | Size | Fit | Confidence |
|-------------|------|-----|------------|

### Prioritization
[Using RICE/ICE/MoSCoW]

## Recommendations
### Strategic Options
| Option | Pros | Cons |
|--------|------|------|

### Recommended Path
[Specific recommendation with rationale]

## Next Steps
1. [Action item]
2. [Action item]
```

## Integration

| Agent | Usage |
|-------|-------|
| ai-pm | Strategic planning |
| competitive-benchmarking | Market analysis |

## Metadata

- **Owner**: Product Strategy Team
- **Created**: 2025-06-15
- **Updated**: 2026-01-10
