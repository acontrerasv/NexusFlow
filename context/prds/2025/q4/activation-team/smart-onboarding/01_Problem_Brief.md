# Problem Brief: Smart Onboarding

> Understanding the activation challenge at NexusFlow.

## Executive Summary

NexusFlow's current onboarding experience is failing to activate new users efficiently. With a 45% activation rate and 12-day average time to first value, we're losing potential long-term customers before they experience the product's core value proposition.

---

## Problem Statement

**New users struggle to reach first value quickly, resulting in low activation rates and missed revenue opportunity.**

### Evidence

| Data Point | Value | Source |
|------------|-------|--------|
| Current Activation Rate | 45% | Product Analytics |
| Target Activation Rate | 65% | Industry Benchmark |
| Time to First Value (TTFV) | 12 days | Product Analytics |
| Target TTFV | 3 days | Best-in-class SaaS |
| Onboarding Completion | 34% | Product Analytics |
| 30-day Churn (Non-activated) | 67% | Cohort Analysis |
| 30-day Churn (Activated) | 12% | Cohort Analysis |

### Impact

- **Revenue Impact**: €892K annual opportunity cost from non-activated users
- **Growth Impact**: Negative word-of-mouth from frustrated signups
- **Efficiency Impact**: CS team spending 40% time on manual onboarding

---

## Root Cause Analysis

### Primary Causes

1. **One-size-fits-all experience** (35% of friction)
   - Same flow for Sales Rep and VP of Sales
   - No industry customization
   - Generic goal setting

2. **CRM connection barrier** (28% of friction)
   - OAuth flow confusing
   - Admin permissions required
   - No alternative path

3. **Blank canvas problem** (22% of friction)
   - Users don't know where to start
   - Templates not discoverable
   - No guidance on first workflow

4. **No value preview** (15% of friction)
   - Can't try before committing
   - No sample data option
   - Abstract value proposition

### Supporting Research

**User Interviews (n=24)**
- "I signed up but had no idea what to do first" - 16/24
- "I needed my IT admin to connect the CRM" - 12/24
- "The templates seemed complicated" - 14/24

**Session Recordings Analysis (n=200)**
- 42% of users stall at CRM connection step
- 31% explore randomly without clear path
- 27% abandon within first session

---

## User Segments Affected

### Most Impacted

| Segment | Activation Rate | TTFV | Size |
|---------|-----------------|------|------|
| Solo practitioners | 32% | 18 days | 45% of signups |
| SMB teams (no ops) | 41% | 14 days | 32% of signups |
| Trial users (no credit card) | 28% | 22 days | 23% of signups |

### Least Impacted

| Segment | Activation Rate | TTFV | Size |
|---------|-----------------|------|------|
| Enterprise with CSM | 78% | 5 days | 8% of signups |
| Referral users | 62% | 8 days | 12% of signups |

---

## Current State Journey

```
Sign Up → Email Verify → CRM Connect → Invite Team → Create Workflow → First Run
   ↓           ↓              ↓             ↓              ↓            ↓
  100%        89%            58%           42%            28%          22%
```

### Drop-off Analysis

| Step | Drop-off | Primary Reason |
|------|----------|----------------|
| Email Verify | 11% | Spam folder, wrong email |
| CRM Connect | 31% | OAuth confusion, admin needed |
| Invite Team | 16% | "I'll do this later" |
| Create Workflow | 14% | Don't know what to build |
| First Run | 6% | Workflow errors |

---

## Business Context

### Strategic Alignment

- **North Star**: Active Workflows Run per Month (120K → 500K)
- **2026 Goal**: 70% activation rate
- **OKR O3**: Dramatically Improve Activation Experience

### Competitive Pressure

| Competitor | Activation Rate | TTFV |
|------------|-----------------|------|
| FlowForce | 58% | 7 days |
| PipelineAI | 62% | 5 days |
| NexusFlow | 45% | 12 days |

---

## Constraints

1. **Technical**: Must integrate with existing auth system
2. **Resource**: Single sprint team available
3. **Timeline**: Must ship before Q4 end
4. **Data**: GDPR compliance for personalization

---

## Success Criteria

| Metric | Current | Target | Measurement |
|--------|---------|--------|-------------|
| Activation Rate | 45% | 65% | 30-day cohort |
| TTFV | 12 days | 3 days | Median |
| Onboarding Completion | 34% | 70% | % completing all steps |
| User Satisfaction | 3.2/5 | 4.5/5 | Post-onboarding survey |

---

## Next Steps

1. Complete JTBD analysis → [02_JTBD.md](./02_JTBD.md)
2. Define solution hypothesis → [03_Solution_Hypothesis.md](./03_Solution_Hypothesis.md)
3. Write full PRD → [04_PRD.md](./04_PRD.md)

---

*Document Owner: Sofia Martinez*
*Last Updated: September 2025*
*Status: Approved*
