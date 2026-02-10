---
name: pipeline-metrics-analyzer
description: Analyzes sales pipeline metrics, conversion rates, deal velocity, and pipeline health indicators for NexusFlow's B2B sales automation context.
---

# Pipeline Metrics Analyzer

## Capabilities

- Calculate pipeline conversion rates
- Analyze deal velocity metrics
- Identify pipeline health indicators
- Segment analysis by stage, source, region
- Forecast pipeline outcomes
- Detect anomalies in pipeline data

## Inputs

| Input | Type | Required | Description |
|-------|------|----------|-------------|
| pipeline_data | object/csv | Yes | Pipeline data to analyze |
| period | string | No | Time period (default: last 30 days) |
| segments | string[] | No | Segments to analyze |
| compare_period | string | No | Period to compare against |

## Outputs

| Output | Type | Description |
|--------|------|-------------|
| metrics_summary | object | Key pipeline metrics |
| stage_analysis | object | Conversion by stage |
| velocity_report | object | Deal velocity analysis |
| health_score | number | Overall pipeline health (0-100) |
| recommendations | string[] | Actionable recommendations |

## Pipeline Metrics Framework

### Key Metrics

| Metric | Definition | Formula | Benchmark |
|--------|------------|---------|-----------|
| Pipeline Value | Total value of active deals | Sum of deal values | Context-dependent |
| Pipeline Coverage | Pipeline vs quota ratio | Pipeline / Quota | 3x-4x |
| Win Rate | % of deals won | Won / (Won + Lost) | 20-30% |
| Avg Deal Size | Average won deal value | Total Won Value / Deals Won | €8,500 |
| Sales Cycle | Days from create to close | Avg days to close | 45 days |
| Velocity | Revenue generated per day | (Deals × Value × Win%) / Cycle | €12,000/day |

### Stage Conversion Benchmarks (NexusFlow)

| Stage | Entry Rate | Exit Rate | Benchmark |
|-------|------------|-----------|-----------|
| Lead | 100% | 40% | 35-45% |
| Qualified | 40% | 60% | 55-65% |
| Proposal | 24% | 50% | 45-55% |
| Negotiation | 12% | 70% | 65-75% |
| Closed Won | 8.4% | - | 8-12% |

## Analysis Templates

### Pipeline Summary

```markdown
## Pipeline Analysis: [Period]

### Overview
| Metric | Value | vs Previous | Trend |
|--------|-------|-------------|-------|
| Total Pipeline | €X | +/-X% | ↑/↓ |
| New Opportunities | X | +/-X% | ↑/↓ |
| Win Rate | X% | +/-Xpp | ↑/↓ |
| Avg Deal Size | €X | +/-X% | ↑/↓ |
| Sales Cycle | X days | +/-X days | ↑/↓ |

### Pipeline Health Score: [X/100]
[Interpretation of score]

### Stage Distribution
| Stage | Count | Value | Conversion |
|-------|-------|-------|------------|
| Lead | X | €X | X% |
| Qualified | X | €X | X% |
| Proposal | X | €X | X% |
| Negotiation | X | €X | X% |

### Recommendations
1. [Recommendation 1]
2. [Recommendation 2]
```

### Velocity Analysis

```markdown
## Velocity Analysis: [Period]

### Current Velocity
Pipeline Velocity = (Opportunities × Avg Deal × Win Rate) / Sales Cycle
                  = (X × €X × X%) / X days
                  = €X/day

### Velocity by Segment
| Segment | Velocity | vs Benchmark |
|---------|----------|--------------|
| Enterprise | €X/day | +/-X% |
| Mid-Market | €X/day | +/-X% |
| SMB | €X/day | +/-X% |

### Velocity Improvement Opportunities
| Lever | Current | Target | Impact |
|-------|---------|--------|--------|
| Increase Win Rate | X% | X% | +€X/day |
| Reduce Cycle | X days | X days | +€X/day |
| Increase Deal Size | €X | €X | +€X/day |
```

## Health Score Calculation

```python
def calculate_health_score(pipeline_data):
    """
    Calculate pipeline health score (0-100)
    """
    scores = {
        'coverage': score_coverage(pipeline_data),      # 0-25
        'balance': score_stage_balance(pipeline_data),   # 0-25
        'velocity': score_velocity(pipeline_data),       # 0-25
        'quality': score_deal_quality(pipeline_data),    # 0-25
    }

    return sum(scores.values())

def score_coverage(data):
    """Pipeline coverage scoring"""
    coverage = data.pipeline_value / data.quota
    if coverage >= 4.0: return 25
    if coverage >= 3.0: return 20
    if coverage >= 2.5: return 15
    if coverage >= 2.0: return 10
    return 5

def score_stage_balance(data):
    """Stage distribution scoring"""
    # Ideal: pyramid shape with more early-stage
    # Penalize inverted funnels
    pass

def score_velocity(data):
    """Velocity vs benchmark scoring"""
    pass

def score_deal_quality(data):
    """Deal quality indicators"""
    pass
```

### Health Score Interpretation

| Score | Rating | Description |
|-------|--------|-------------|
| 80-100 | Excellent | Pipeline is healthy, well-balanced |
| 60-79 | Good | Minor improvements needed |
| 40-59 | Needs Attention | Significant gaps to address |
| 20-39 | At Risk | Major issues affecting performance |
| 0-19 | Critical | Urgent intervention required |

## Anomaly Detection

### Anomaly Types

| Anomaly | Detection | Action |
|---------|-----------|--------|
| Stale Deals | No activity >14 days | Review/remove |
| Stuck Stage | In stage >2x average | Investigate |
| Unusual Value | >3 std dev from mean | Verify |
| Low Activity | <5 activities | Re-engage |
| Sudden Drop | >30% week-over-week | Investigate |

## NexusFlow Context

### Current Pipeline State (Q1 2026)
| Metric | Value | Target | Status |
|--------|-------|--------|--------|
| Total Pipeline | €4.2M | €5.0M | 🟡 |
| Coverage | 2.8x | 3.5x | 🟡 |
| Win Rate | 24% | 28% | 🟡 |
| Avg Deal Size | €7,200 | €8,500 | 🟡 |
| Sales Cycle | 52 days | 45 days | 🔴 |

### Segment Performance
| Segment | Pipeline | Win Rate | Cycle |
|---------|----------|----------|-------|
| Enterprise | €1.8M | 18% | 78 days |
| Professional | €1.6M | 26% | 42 days |
| Starter | €0.8M | 32% | 28 days |

## Usage Example

```python
# Analyze pipeline metrics
result = pipeline_metrics_analyzer.analyze(
    pipeline_data=current_pipeline,
    period="2026-01",
    segments=["enterprise", "professional"],
    compare_period="2025-12"
)

# Access results
print(f"Health Score: {result.health_score}")
print(f"Velocity: €{result.metrics_summary.velocity}/day")
for rec in result.recommendations:
    print(f"- {rec}")
```

## Integration

| Agent | Usage |
|-------|-------|
| ai-data-analyst | Primary user |
| ai-pm | Strategic context |
| product-usage-analyst | Correlation with product usage |

## Metadata

- **Owner**: Data Team
- **Created**: 2025-07-01
- **Updated**: 2026-01-10
