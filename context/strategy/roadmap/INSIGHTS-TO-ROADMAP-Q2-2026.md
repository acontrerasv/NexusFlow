# Insights to Roadmap: Q2 2026

> How data insights shaped our Q2 2026 roadmap decisions.

## Executive Summary

This document traces the connection between Q1 2026 insights and Q2 2026 roadmap priorities. Every initiative on our roadmap is backed by evidence.

---

## Insight #1: Enterprise Churn Crisis

### The Data

| Metric | Value | Impact |
|--------|-------|--------|
| Enterprise churn | 12.3% | Critical |
| Enterprise MRR at risk | €339K/year | Series B threat |
| Integration-related churn | 28% of total | Root cause #1 |

### Root Cause Analysis

**Primary**: Integration complexity (28%)
- CRM OAuth completion: 56%
- Avg setup time: 4.5 hours
- Support tickets: 342/month

**Secondary**: Feature gaps (25%)
- Missing SAML SSO
- No audit logs
- Basic workflow conditions

### Roadmap Response

| Initiative | Team | Q2 Target | Expected Impact |
|------------|------|-----------|-----------------|
| CRM Sync v2 | Integration | June | -50% integration churn |
| SAML SSO | Platform | May | Enterprise blocker removed |
| Audit Logs | Platform | June | Compliance requirement |
| Enterprise Support Hours | Support | April | 24/7 coverage |

### Success Metrics

- Enterprise churn: 12.3% → <8%
- CRM OAuth completion: 56% → 75%
- Setup time: 4.5h → 1.5h

---

## Insight #2: Activation Failure

### The Data

| Metric | Value | Target | Gap |
|--------|-------|--------|-----|
| Activation rate | 45% | 65% | -20pp |
| TTFV | 12 days | 3 days | +9 days |
| Biggest drop-off | CRM step (26%) | - | Critical |

### Root Cause Analysis

**CRM Connection Barrier**
- 26% drop at OAuth
- Users need admin approval
- Errors unhelpful

**Blank Canvas Problem**
- 42% "don't know where to start"
- Templates underutilized
- No AI guidance

### Roadmap Response

| Initiative | Team | Q2 Target | Expected Impact |
|------------|------|-----------|-----------------|
| Skip CRM Option | Activation | April | +12pp activation |
| AI Workflow Creation | Engagement | May | +8pp activation |
| Guided Onboarding v2 | Activation | May | -3 days TTFV |
| OAuth Flow Redesign | Integration | April | +15pp CRM completion |

### Success Metrics

- Activation rate: 45% → 55%
- TTFV: 12 days → 6 days
- CRM completion: 34% → 45%

---

## Insight #3: AI Features Drive Retention

### The Data

| Metric | AI Users | Non-AI Users | Lift |
|--------|----------|--------------|------|
| 30-day retention | 92% | 78% | +14pp |
| Workflows created | 12.4 | 6.2 | +100% |
| NPS | 52 | 34 | +18 |

But only 12% of users have tried AI features.

### Root Cause Analysis

**Low Discovery**
- AI features hidden in menus
- No prompts to try AI
- Limited use cases

### Roadmap Response

| Initiative | Team | Q2 Target | Expected Impact |
|------------|------|-----------|-----------------|
| AI Everywhere | Engagement | June | 2x AI adoption |
| AI Onboarding Path | Activation | May | AI users at start |
| AI Workflow Templates | Engagement | June | Easy AI entry |

### Success Metrics

- AI feature adoption: 12% → 30%
- AI user retention: maintain 92%

---

## Insight #4: UX Friction Points

### The Data

From UX Audit:
- 12 critical issues identified
- Workflow builder: 11 issues
- Mobile: "broken" experience
- Dashboard loading: 2-3s blank

### Root Cause Analysis

**Workflow Builder**
- No undo functionality
- Blank canvas intimidating
- Status unclear

**General UX**
- Loading states missing
- Error messages unhelpful
- Mobile neglected

### Roadmap Response

| Initiative | Team | Q2 Target | Expected Impact |
|------------|------|-----------|-----------------|
| Workflow Builder v2 | Engagement | June | Address 8 issues |
| Dashboard Loading States | Platform | April | Quick win |
| Error Message Improvements | Platform | April | -30% support tickets |
| Mobile Monitoring View | Frontend | June | Mobile usability |

### Success Metrics

- Workflow builder NPS: +10 points
- Dashboard bounce rate: -50%
- Mobile session length: 2x

---

## Insight #5: NRR Below Target

### The Data

| Metric | Current | Target | Gap |
|--------|---------|--------|-----|
| NRR | 108% | 125% | -17pp |
| Expansion revenue | 14.8% | 20% | -5.2pp |
| Upsell conversion | 8% | 15% | -7pp |

### Root Cause Analysis

**Limited Expansion Triggers**
- No usage-based pricing
- Add-ons not launched
- Upgrade path unclear

**Value Not Demonstrated**
- ROI not visible
- No business impact metrics
- Limited reporting

### Roadmap Response

| Initiative | Team | Q2 Target | Expected Impact |
|------------|------|-----------|-----------------|
| Usage Alerts | Retention | April | Proactive expansion |
| Business Impact Dashboard | Platform | June | Demonstrate value |
| Upgrade Prompts | Growth | May | +5pp conversion |

### Success Metrics

- NRR: 108% → 112%
- Expansion revenue: +20%
- Upsell conversion: 8% → 12%

---

## Q2 2026 Roadmap Summary

### April (Month 1)

| Initiative | Team | Priority |
|------------|------|----------|
| Skip CRM Option | Activation | P0 |
| OAuth Flow Redesign | Integration | P0 |
| Dashboard Loading States | Platform | P1 |
| Error Message Improvements | Platform | P1 |
| Enterprise Support Hours | Support | P0 |
| Usage Alerts | Retention | P1 |

### May (Month 2)

| Initiative | Team | Priority |
|------------|------|----------|
| SAML SSO | Platform | P0 |
| AI Workflow Creation | Engagement | P0 |
| Guided Onboarding v2 | Activation | P0 |
| AI Onboarding Path | Activation | P1 |
| Upgrade Prompts | Growth | P2 |

### June (Month 3)

| Initiative | Team | Priority |
|------------|------|----------|
| CRM Sync v2 | Integration | P0 |
| Audit Logs | Platform | P0 |
| AI Everywhere | Engagement | P1 |
| AI Workflow Templates | Engagement | P1 |
| Workflow Builder v2 | Engagement | P1 |
| Business Impact Dashboard | Platform | P2 |
| Mobile Monitoring View | Frontend | P2 |

---

## Investment Allocation

| Focus Area | % of Engineering | Rationale |
|------------|-----------------|-----------|
| Enterprise Retention | 35% | Critical for Series B |
| Activation | 30% | Drives growth |
| AI Features | 20% | Differentiation |
| UX Improvements | 15% | Foundation |

---

## Risk Mitigation

| Risk | Mitigation |
|------|------------|
| CRM Sync v2 delays | Start early, phased rollout |
| SAML complexity | Use established library |
| AI adoption low | Strong launch campaign |
| Resource constraints | Ruthless prioritization |

---

## Tracking

### Weekly

- Initiative progress
- Blockers
- Metric movement

### Monthly

- OKR check-in
- Roadmap adjustments
- Resource reallocation

### Quarterly

- Full roadmap review
- Insight refresh
- Next quarter planning

---

*Document Owner: Product Team*
*Last Updated: January 2026*
