# Discovery Summary: Onboarding Simplificado

## Metadata
- **Date**: 2026-01-26
- **Orchestrated By**: discovery-orchestrator v1.4.0
- **Depth**: Quick
- **Feature Area**: Onboarding / Activation
- **Team**: Activation

---

## Executive Summary

NexusFlow's onboarding is a critical bottleneck preventing activation and retention. Despite the Smart Onboarding v1 shipped in Q4 2025, **only 31% of signups reach activation** (3+ workflow runs), with **Time to First Value at 12 days** vs. a 3-day target. The primary friction points are:

1. **CRM Connection Barrier** - 26% of users drop off at this step (342 support tickets/month)
2. **Blank Canvas Problem** - 42% cite "don't know where to start"
3. **No Progress Saving** - 35% abandon mid-flow and lose progress

Simplifying onboarding represents a **€1.8-2.8M ARR opportunity** through improved activation, plus **€120-180K recovered MRR** through reduced churn. This is critical for Series B readiness (Q4 2026).

---

## Strategic Context

### OKR Alignment

| OKR | Alignment | Impact |
|-----|-----------|--------|
| **O3: Dramatically Improve Activation** | **Direct** | Primary KR: Activation 45%→55%, TTFV 12→6 days |
| O1: Reduce Enterprise Churn | High | Integration complexity = 28% of churn |
| O4: AI as Differentiator | Medium | AI-assisted onboarding drives 2.3x faster activation |
| O2: Grow Enterprise Customer Base | Medium | Enterprise TTFV 18 days blocks growth |

### Strategic Priority

**HIGH** - Activation is the #3 company OKR (O3) and directly impacts:
- Series B metrics (NRR 108% → 125% target)
- Enterprise churn crisis (12.3% monthly)
- Net revenue retention

### Prior Art

Smart Onboarding v1 (Q4 2025) delivered:
- TTFV: 12 days → 4.2 days ✅
- Activation: 45% → 52% (below 65% target) ⚠️
- Onboarding completion: 34% → 68% ✅

**Remaining gaps** justify this initiative.

---

## Problem Space

### Problem Statement

> Users who sign up for NexusFlow cannot quickly reach their first value moment because the onboarding process requires CRM connection (blocking 26%), offers no guidance on where to start (confusing 42%), and doesn't save progress (frustrating 35%). This results in 12-day TTFV vs. 3-day target and 31% activation vs. 65% target.

### Evidence

#### Quantitative
| Metric | Current | Target | Gap |
|--------|---------|--------|-----|
| Activation Rate | 31% | 65% | -34pp |
| TTFV (all users) | 12 days | 3 days | +9 days |
| TTFV (Enterprise) | 18 days | 7 days | +11 days |
| CRM Connection Rate | 34% | 50% | -16pp |
| Drop-off at CRM step | 26% | <10% | +16pp |
| Onboarding NPS | 3.2/5 | 4.5/5 | -1.3 |

#### Qualitative
- "I signed up but had no idea what to do first" - User interview
- "I needed my IT admin to connect the CRM" - 50% of users
- "The templates seemed complicated" - User interview
- 342 support tickets/month about CRM connection issues

#### Competitive
| Competitor | Activation Rate | TTFV |
|------------|-----------------|------|
| FlowForce | 58% | 7 days |
| PipelineAI | 62% | 5 days |
| **NexusFlow** | **31%** | **12 days** |

### Impact Assessment

| Dimension | Impact | Confidence |
|-----------|--------|------------|
| Users Affected | 69% of signups don't activate | High |
| Business Impact | €1.8-2.8M ARR opportunity | Medium |
| Strategic Value | Critical for Series B | High |
| Effort | Medium (building on v1 foundation) | Medium |

---

## User Insights

### Target Personas

| Persona | Size | Activation | TTFV | Key Issue |
|---------|------|------------|------|-----------|
| **Solo Practitioner** | 45% | 32% | 18 days | Can't get CRM admin approval |
| **SMB Team (no ops)** | 32% | 41% | 14 days | Don't know where to start |
| **Trial User (no CC)** | 23% | 28% | 22 days | "Just exploring, not ready" |

### Pain Points

1. **CRM Connection is Mandatory Blocker** (28% of friction)
   - 26% drop-off at this step
   - OAuth errors unhelpful (342 tickets/month)
   - Admin approval required (28% can't proceed independently)

2. **Blank Canvas Problem** (22% of friction)
   - 42% stall saying "don't know where to start"
   - Templates not discoverable (58% browse, only 45% use)
   - Users spend 3.2 minutes staring at blank workflow

3. **Progress Not Saved** (Critical UX issue)
   - 35% abandon mid-flow and must restart
   - No resume capability across sessions
   - State lost on page refresh

4. **No Value Preview** (15% of friction)
   - Can't try before committing time/data
   - Abstract value proposition
   - 22% drop before even starting onboarding

### Jobs to Be Done

| Job | Current Solution | Gap | Priority |
|-----|------------------|-----|----------|
| Get oriented quickly | Generic dashboard | No guidance, unclear next steps | Critical |
| Connect CRM without IT help | OAuth flow | Admin required for 28%, errors unhelpful | Critical |
| Create first automation | Blank workflow builder | No templates surfaced, "don't know where to start" | High |
| Understand value before investing time | No sample data | Must commit data before seeing value | Medium |

---

## Data Insights

### Activation Funnel (Q1 2026)

```
Sign Up → Email Verify → Start Onboarding → CRM Connect → Workflow → First Run → Activated
  100%       94%             78%              52%          45%        38%        31%
             ↓6%             ↓22%             ↓26%         ↓7%        ↓7%        ↓9%
```

### Key Metrics

| Metric | Current | Benchmark | Gap |
|--------|---------|-----------|-----|
| Drop-off before onboarding | 22% | <10% | +12pp |
| Drop-off at CRM | 26% | <10% | +16pp |
| Template usage | 45% | 70%+ | -25pp |
| Same-session workflow run | 85% success | N/A | Best practice |
| >24h to first run | 35% success | N/A | Critical decay |

### Trends

- **TTFV increased** from 11 days (Q4 2025) to 12 days (Q1 2026) - wrong direction
- **Enterprise TTFV** at 18 days vs. 7-day target
- **AI-assisted users** activate 2.3x faster
- **Users who spend >5 minutes** on CRM setup are likely to complete

### Segment Performance

| Segment | Activation | Status |
|---------|------------|--------|
| Referral users | 52% | Best performing |
| Demo-trial users | 48% | Pre-educated |
| Starter plan | 28% | SMB struggling |
| Paid (Google Ads) | 25% | Lowest quality |

---

## Recommendations

### Recommended Path Forward

**Iterate on Smart Onboarding v1** with targeted improvements:

1. **Allow CRM Skip** - Let users create workflows without CRM connection
   - Impact: Unblock 26% drop-off
   - Risk: May reduce long-term retention (guardrail: >30% CRM connection rate)

2. **AI-First Workflow Creation** - "Tell us what you want to automate"
   - Impact: Address 42% "don't know where to start"
   - Evidence: AI users activate 2.3x faster

3. **Save Progress** - Persistent onboarding state
   - Impact: Address 35% who abandon and must restart
   - Complexity: Low (session storage + DB)

4. **Template Recommendations** - Pre-select based on role/industry
   - Impact: Increase template usage from 45% to 70%+
   - Evidence: 97% success rate with templates vs. 91.5% blank canvas

### Options Considered

| Option | Pros | Cons | Recommendation |
|--------|------|------|----------------|
| Iterate on v1 | Builds on foundation, faster | May not fully solve Enterprise TTFV | **Recommended** |
| Full redesign | Clean slate | High effort, delays | Not recommended |
| CRM Sync v2 first | Solves integration root cause | Longer timeline, different team | Parallel initiative |

### Open Questions

- [ ] Will users who skip CRM retain at acceptable rates?
- [ ] Which role-based paths (Sales Rep, Manager, Ops) drive most lift?
- [ ] Should mobile onboarding be separate MVP?
- [ ] Is 3+ workflow runs the right activation definition?

### Suggested Next Steps

1. **Immediate**: Begin PRD for "Onboarding Simplificado" (this discovery informs it)
2. **Short-term**: User interviews (n=12) on goal-setting wizard engagement
3. **Short-term**: Prototype testing (n=8) on role selection accuracy
4. **Medium-term**: A/B test CRM skip vs. required flow

---

## Appendix

### Sources Referenced

- `/context/prds/2025/q4/activation-team/smart-onboarding/` - Smart Onboarding v1 PRD
- `/context/data/insights/ACTIVATION-DROPOFF-ANALYSIS-Q1-2026.md` - Funnel analysis
- `/context/data/insights/Q1-2026-PRODUCT-USAGE-SUMMARY.md` - Usage metrics
- `/context/data/churn-analysis/CHURN-ANALYSIS-Q1-2026-COMPLETE.md` - Churn deep-dive
- `/context/data/ux/UX-AUDIT-FINDINGS-Q1-2026.md` - UX audit
- `/context/strategy/okr/2026/Q2-OKRS.md` - Company OKRs
- `/context/strategy/roadmap/INSIGHTS-TO-ROADMAP-Q2-2026.md` - Roadmap rationale

### Key Metrics Summary

| Category | Metric | Current | Target |
|----------|--------|---------|--------|
| Activation | Activation Rate | 31% | 65% |
| Activation | TTFV | 12 days | 3 days |
| Funnel | CRM Connection | 34% | 50% |
| Funnel | Onboarding Completion | 68% | 85% |
| Satisfaction | Onboarding NPS | 3.2/5 | 4.5/5 |
| Business | Onboarding-related churn | €18,607 MRR | €5,000 MRR |
