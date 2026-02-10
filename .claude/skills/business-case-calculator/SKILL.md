---
name: business-case-calculator
description: Calculates business impact, ROI, and financial projections for product initiatives. Helps prioritize features based on quantified business value.
---

# Business Case Calculator

## Capabilities

- Calculate ROI and payback period
- Estimate revenue impact
- Model cost savings
- Project customer impact
- Compare initiative economics
- Generate business case documents

## Inputs

| Input | Type | Required | Description |
|-------|------|----------|-------------|
| initiative | object | Yes | Initiative details |
| costs | object | Yes | Development and operational costs |
| benefits | object | Yes | Expected benefits |
| timeframe | number | No | Analysis period in months (default: 12) |
| discount_rate | number | No | For NPV calculation (default: 10%) |

## Outputs

| Output | Type | Description |
|--------|------|-------------|
| roi | number | Return on Investment (%) |
| npv | number | Net Present Value |
| payback_months | number | Months to break even |
| revenue_impact | object | Revenue projections |
| cost_savings | object | Cost reduction projections |
| recommendation | string | Go/No-go recommendation |

## Business Case Framework

### Cost Categories

| Category | Description | Examples |
|----------|-------------|----------|
| Development | Engineering time | Salaries, contractors |
| Infrastructure | Cloud/hosting | AWS, databases |
| Operations | Ongoing support | Support staff, maintenance |
| Opportunity | Alternative use of resources | Other features not built |

### Benefit Categories

| Category | Description | Examples |
|----------|-------------|----------|
| Revenue Increase | New/expanded revenue | New customers, upgrades |
| Churn Reduction | Retained revenue | Prevented cancellations |
| Cost Savings | Reduced expenses | Automation, efficiency |
| Productivity | Time savings | Hours saved × rate |

## Calculation Models

### ROI Calculation

```python
def calculate_roi(benefits, costs, timeframe_months=12):
    """
    Calculate Return on Investment

    ROI = (Net Benefit / Total Cost) × 100
    """
    total_benefits = sum_benefits(benefits, timeframe_months)
    total_costs = sum_costs(costs)

    net_benefit = total_benefits - total_costs
    roi = (net_benefit / total_costs) * 100

    return round(roi, 1)
```

### NPV Calculation

```python
def calculate_npv(cash_flows, discount_rate=0.10):
    """
    Calculate Net Present Value

    NPV = Σ (Cash Flow_t / (1 + r)^t)
    """
    npv = 0
    for t, cf in enumerate(cash_flows):
        npv += cf / ((1 + discount_rate) ** t)
    return round(npv, 2)
```

### Payback Period

```python
def calculate_payback(costs, monthly_benefit):
    """
    Calculate months to recover investment
    """
    total_cost = sum_costs(costs)
    payback_months = total_cost / monthly_benefit
    return round(payback_months, 1)
```

## Revenue Impact Models

### Churn Reduction Model

```python
def model_churn_reduction(
    current_mrr: float,
    current_churn_rate: float,
    target_churn_rate: float,
    months: int = 12
) -> dict:
    """
    Model revenue saved from churn reduction
    """
    monthly_churn_reduction = current_churn_rate - target_churn_rate
    monthly_revenue_saved = current_mrr * monthly_churn_reduction

    total_saved = 0
    mrr = current_mrr

    for month in range(months):
        saved_this_month = mrr * monthly_churn_reduction
        total_saved += saved_this_month
        mrr = mrr * (1 - target_churn_rate)  # Compound effect

    return {
        "monthly_average": total_saved / months,
        "total_12_month": total_saved,
        "arr_impact": total_saved * 12 / months
    }
```

### Expansion Revenue Model

```python
def model_expansion_revenue(
    customer_base: int,
    expansion_rate: float,
    avg_expansion_value: float,
    months: int = 12
) -> dict:
    """
    Model revenue from upgrades/expansion
    """
    monthly_expansions = customer_base * expansion_rate
    monthly_revenue = monthly_expansions * avg_expansion_value

    return {
        "monthly": monthly_revenue,
        "annual": monthly_revenue * 12,
        "customers_expanding": monthly_expansions * months
    }
```

### New Customer Model

```python
def model_new_customers(
    conversion_improvement: float,
    current_conversions: int,
    avg_deal_value: float,
    months: int = 12
) -> dict:
    """
    Model revenue from improved conversion
    """
    additional_conversions = current_conversions * conversion_improvement
    monthly_revenue = additional_conversions * avg_deal_value

    return {
        "additional_customers": additional_conversions * months,
        "monthly_revenue": monthly_revenue,
        "annual_revenue": monthly_revenue * 12
    }
```

## NexusFlow Benchmarks

### Cost Benchmarks

| Resource | Monthly Cost | Notes |
|----------|-------------|-------|
| Senior Engineer | €8,500 | Fully loaded |
| Mid Engineer | €6,500 | Fully loaded |
| Product Manager | €7,500 | Fully loaded |
| Designer | €6,000 | Fully loaded |
| Infrastructure | €2,500/service | AWS average |

### Value Benchmarks

| Metric | Value | Source |
|--------|-------|--------|
| Avg MRR per Customer | €285 | Q1 2026 |
| Enterprise MRR | €1,450 | Q1 2026 |
| Customer Acquisition Cost | €850 | 2025 avg |
| Lifetime Value (SMB) | €3,420 | 12-month |
| Lifetime Value (Enterprise) | €17,400 | 12-month |

### Churn Impact

| Churn Type | Monthly Impact |
|------------|----------------|
| 1 Enterprise customer | €1,450 MRR lost |
| 1% Enterprise churn | €2,262 MRR lost |
| 1% Total churn | €5,264 MRR lost |

## Output Format

### Business Case Summary

```markdown
# Business Case: [Initiative Name]

## Executive Summary

| Metric | Value |
|--------|-------|
| **ROI** | **245%** |
| **NPV** | **€142,500** |
| **Payback** | **4.2 months** |
| **Recommendation** | **PROCEED** |

## Investment Required

| Category | Amount | Timeline |
|----------|--------|----------|
| Development | €85,000 | 3 months |
| Infrastructure | €12,000 | Year 1 |
| Operations | €18,000 | Year 1 |
| **Total** | **€115,000** | - |

### Development Breakdown
| Resource | Months | Cost |
|----------|--------|------|
| 2 Engineers | 3 | €51,000 |
| 1 PM | 2 | €15,000 |
| 1 Designer | 2 | €12,000 |
| QA | 1 | €7,000 |

## Expected Benefits

### Revenue Impact
| Source | Monthly | Annual |
|--------|---------|--------|
| Churn Reduction | €8,500 | €102,000 |
| Expansion Revenue | €4,200 | €50,400 |
| New Customers | €6,800 | €81,600 |
| **Total** | **€19,500** | **€234,000** |

### Cost Savings
| Source | Monthly | Annual |
|--------|---------|--------|
| Support Reduction | €2,100 | €25,200 |
| Manual Process | €1,500 | €18,000 |
| **Total** | **€3,600** | **€43,200** |

### Total Benefits
- **Year 1**: €277,200
- **Year 2**: €312,000 (with growth)
- **3-Year Total**: €901,200

## Financial Analysis

### ROI Calculation
```
ROI = (Benefits - Costs) / Costs × 100
ROI = (€277,200 - €115,000) / €115,000 × 100
ROI = 141% (Year 1)
```

### NPV Analysis (10% discount rate)
| Year | Cash Flow | Discounted |
|------|-----------|------------|
| 0 | -€85,000 | -€85,000 |
| 1 | €162,200 | €147,455 |
| 2 | €197,000 | €162,810 |
| **NPV** | | **€225,265** |

### Payback Period
```
Monthly Benefit = €23,100
Total Investment = €115,000
Payback = 115,000 / 23,100 = 5.0 months
```

## Sensitivity Analysis

| Scenario | ROI | NPV | Payback |
|----------|-----|-----|---------|
| Base Case | 141% | €225K | 5.0 mo |
| Conservative (-20%) | 93% | €160K | 6.2 mo |
| Optimistic (+20%) | 189% | €290K | 4.2 mo |
| Delayed Benefits (+2mo) | 118% | €195K | 6.5 mo |

## Risks to Benefits

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| Lower adoption | -30% benefits | Medium | Phased rollout |
| Technical delays | +2 months cost | Low | Buffer in timeline |
| Market changes | -20% new customers | Low | Monitor and adjust |

## Recommendation

**PROCEED** with initiative based on:
- Strong ROI (141%) exceeding 50% threshold
- Quick payback (5 months) within 6-month target
- Positive NPV under all scenarios
- Alignment with O1 (churn reduction) priority

## Appendix
[Detailed calculations and assumptions]
```

## Usage Example

```python
# Calculate business case
result = business_case_calculator.calculate(
    initiative={
        "name": "CRM Sync v2",
        "team": "integration"
    },
    costs={
        "development": 85000,
        "infrastructure": 12000,
        "operations": 18000
    },
    benefits={
        "churn_reduction": {
            "current_rate": 0.123,
            "target_rate": 0.08,
            "affected_mrr": 225000
        },
        "expansion": {
            "rate": 0.05,
            "value": 500
        }
    },
    timeframe=12
)

print(f"ROI: {result.roi}%")
print(f"Payback: {result.payback_months} months")
print(f"Recommendation: {result.recommendation}")
```

## Integration

| Agent | Usage |
|-------|-------|
| ai-pm | Strategic decisions |
| ai-data-analyst | Impact modeling |

## Metadata

- **Owner**: Finance & Product Team
- **Created**: 2025-08-01
- **Updated**: 2026-01-12
