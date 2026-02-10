---
name: okr-alignment-checker
description: Validates alignment between product initiatives (PRDs, features, projects) and company OKRs. Ensures work contributes to strategic objectives and helps prioritize based on OKR impact.
---

# OKR Alignment Checker

## Capabilities

- Check initiative alignment to OKRs
- Score alignment strength (0-100)
- Identify best-fit OKRs for initiatives
- Flag misaligned work
- Calculate OKR coverage
- Suggest alignment improvements

## Inputs

| Input | Type | Required | Description |
|-------|------|----------|-------------|
| initiative | object | Yes | Initiative to check (PRD, feature, project) |
| okrs | object | No | OKRs to check against (default: current quarter) |
| threshold | number | No | Minimum alignment score (default: 60) |

## Outputs

| Output | Type | Description |
|--------|------|-------------|
| aligned | boolean | Whether initiative is sufficiently aligned |
| score | number | Alignment score (0-100) |
| primary_okr | object | Best matching OKR |
| secondary_okrs | array | Other aligned OKRs |
| gaps | array | Alignment gaps identified |
| recommendations | array | Suggestions for better alignment |

## NexusFlow Q2 2026 OKRs

### Company OKRs

```yaml
O1: Reduce enterprise churn to sustainable levels
  KR1: Reduce enterprise churn rate from 12.3% to 5%
  KR2: Achieve 90% enterprise customer health score
  KR3: Reduce integration-related churn by 50%
  KR4: Achieve <5 day resolution for critical enterprise issues

O2: Accelerate enterprise customer growth
  KR1: Grow enterprise customers from 156 to 312
  KR2: Increase enterprise pipeline coverage to 4x
  KR3: Reduce enterprise sales cycle from 78 to 60 days
  KR4: Launch 3 enterprise-specific features

O3: Improve product-led growth metrics
  KR1: Increase activation rate from 45% to 65%
  KR2: Reduce time to first value from 12 days to 3 days
  KR3: Improve DAU/MAU ratio from 26% to 35%
  KR4: Achieve NPS of 45+

O4: Expand revenue through retention and expansion
  KR1: Increase NRR from 108% to 115%
  KR2: Launch usage-based pricing tier
  KR3: Achieve 25% attach rate for add-on modules
  KR4: Reduce voluntary downgrades by 30%
```

### Team-Level OKRs

```yaml
Activation Team:
  O: Dramatically improve new user activation
  KRs:
    - Reduce TTFV from 12 to 3 days
    - Increase onboarding completion from 52% to 75%
    - Achieve 65% 7-day activation rate

Retention Team:
  O: Build proactive retention capabilities
  KRs:
    - Implement usage-based health scoring
    - Launch automated engagement campaigns
    - Reduce at-risk accounts by 40%

Integration Team:
  O: Make NexusFlow the easiest platform to integrate
  KRs:
    - Reduce CRM setup time by 60%
    - Launch 5 new native integrations
    - Achieve 80% sync success rate

Engagement Team:
  O: Increase core feature adoption
  KRs:
    - Increase workflow builder adoption to 80%
    - Launch AI workflow templates
    - Achieve 50% AI feature adoption
```

## Alignment Scoring

### Scoring Algorithm

```python
def calculate_alignment_score(initiative, okrs):
    """
    Calculate alignment score (0-100)
    """
    scores = []

    # Direct impact (50%)
    direct_score = score_direct_impact(initiative, okrs)
    scores.append(('direct', direct_score, 0.50))

    # Metric alignment (30%)
    metric_score = score_metric_alignment(initiative, okrs)
    scores.append(('metric', metric_score, 0.30))

    # Strategic fit (20%)
    strategic_score = score_strategic_fit(initiative, okrs)
    scores.append(('strategic', strategic_score, 0.20))

    return sum(score * weight for _, score, weight in scores)

def score_direct_impact(initiative, okrs):
    """
    Score based on direct KR impact
    """
    # Check if initiative metrics map to KRs
    # Higher score if initiative success = KR movement
    pass

def score_metric_alignment(initiative, okrs):
    """
    Score based on metric overlap
    """
    # Compare initiative metrics to KR metrics
    # Higher score for direct metric matches
    pass

def score_strategic_fit(initiative, okrs):
    """
    Score based on objective alignment
    """
    # Check if initiative problem space matches O focus
    pass
```

### Alignment Levels

| Score | Level | Interpretation |
|-------|-------|----------------|
| 80-100 | Strong | Direct KR impact, high priority |
| 60-79 | Good | Clear alignment, should proceed |
| 40-59 | Moderate | Some alignment, consider scope |
| 20-39 | Weak | Limited alignment, deprioritize |
| 0-19 | None | No alignment, don't proceed |

## Alignment Patterns

### High Alignment Example
```yaml
Initiative: "CRM Sync Improvements"
Primary OKR: O1-KR3 (Reduce integration-related churn by 50%)
Secondary OKRs:
  - O2-KR4 (Enterprise-specific features)
  - O3-KR2 (Reduce TTFV)
Alignment Score: 92

Rationale:
- Direct metric impact: Integration churn → KR3
- Problem space matches O1 focus
- Also benefits enterprise (O2) and activation (O3)
```

### Weak Alignment Example
```yaml
Initiative: "Dark Mode UI"
Primary OKR: None identified
Secondary OKRs:
  - O3-KR4 (NPS) - weak connection
Alignment Score: 28

Rationale:
- No direct KR impact
- Not addressing current strategic priorities
- Nice-to-have, not aligned to objectives
Recommendation: Defer to future quarter or deprioritize
```

## Output Format

### Alignment Report

```markdown
# OKR Alignment Report

## Initiative
**Name**: [Initiative Name]
**Team**: [Team]
**Type**: [PRD/Feature/Project]

## Alignment Summary

| Aspect | Score | Status |
|--------|-------|--------|
| **Overall Alignment** | **78/100** | **ALIGNED** |
| Direct Impact | 85/100 | ✅ Strong |
| Metric Alignment | 70/100 | ✅ Good |
| Strategic Fit | 75/100 | ✅ Good |

## Primary OKR Alignment

### O1-KR3: Reduce integration-related churn by 50%

| Criterion | Assessment |
|-----------|------------|
| Problem Space | ✅ Integration complexity is root cause |
| Metric Impact | ✅ Success metric maps to KR |
| Target Audience | ✅ Enterprise focus aligns |

**Impact Estimate**: High - Could contribute 30-40% of KR target

## Secondary OKR Alignments

### O2-KR4: Launch 3 enterprise-specific features
- Contribution: This is 1 of 3 required features
- Alignment Score: 65

### O3-KR2: Reduce time to first value
- Contribution: Faster CRM setup reduces TTFV
- Alignment Score: 55

## Gaps Identified

1. **No direct O4 alignment**: Consider revenue expansion angle
2. **Missing NPS connection**: Could improve satisfaction

## Recommendations

1. **Strengthen O4 alignment**: Add upsell opportunity post-CRM setup
2. **Track NPS impact**: Add NPS as secondary metric
3. **Document contribution**: Explicit KR target contribution in PRD

## Conclusion

Initiative is **well-aligned** with company strategy. Primary focus
on O1 (churn reduction) with secondary benefits to O2 and O3.
Recommend proceeding with suggested enhancements.
```

## Usage Example

```python
# Check initiative alignment
result = okr_alignment_checker.check(
    initiative={
        "name": "Dashboard Redesign",
        "team": "activation",
        "metrics": ["activation_rate", "time_to_first_value"],
        "problem": "Users struggle to understand dashboard",
        "impact": "Improve activation and retention"
    },
    threshold=60
)

# Check results
if result.aligned:
    print(f"Aligned to {result.primary_okr.id}")
else:
    print("Initiative needs better OKR alignment")
    for rec in result.recommendations:
        print(f"- {rec}")
```

## Integration

| Agent | Usage |
|-------|-------|
| ai-pm | Strategic planning |
| product-manager | PRD validation |

| Skill | Usage |
|-------|-------|
| prd-compliance-validator | PRD validation flow |

## Metadata

- **Owner**: Product Team
- **Created**: 2025-07-15
- **Updated**: 2026-01-10
