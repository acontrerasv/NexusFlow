# Activation Drop-off Analysis Q1 2026

> Deep analysis of where and why users drop off during activation.

## Executive Summary

**Problem**: Only 31% of signups reach activation (3+ workflow runs).

**Biggest Drop-offs**:
1. Before starting onboarding: 22%
2. At CRM connection: 26%
3. At first workflow creation: 7%

**Root Causes**:
- Unclear value proposition
- Complex CRM OAuth flow
- Lack of guidance

---

## Activation Funnel

### Detailed Funnel Analysis

| Step | Users | Cumulative | Step Conv. | Drop-off |
|------|-------|------------|------------|----------|
| 1. Signed Up | 2,450 | 100% | - | - |
| 2. Verified Email | 2,303 | 94% | 94% | 6% |
| 3. Completed Profile | 2,156 | 88% | 94% | 6% |
| 4. Started Onboarding | 1,911 | 78% | 89% | 11% |
| 5. Selected Use Case | 1,764 | 72% | 92% | 8% |
| 6. Connected CRM | 1,274 | 52% | 72% | **20%** |
| 7. Created Workflow | 1,103 | 45% | 87% | 13% |
| 8. First Run | 931 | 38% | 84% | 16% |
| 9. Second Run | 833 | 34% | 89% | 11% |
| 10. Activated (3+ runs) | 760 | 31% | 91% | 9% |

---

## Drop-off Point #1: Before Onboarding (22%)

### Where They Stop

| Last Action | % of Drop-offs |
|-------------|----------------|
| Verified email, never returned | 45% |
| Visited homepage once | 32% |
| Started profile, abandoned | 23% |

### Time to Drop-off

| Timeframe | % |
|-----------|---|
| Within 1 hour | 38% |
| 1-24 hours | 35% |
| 1-7 days | 27% |

### User Characteristics

| Characteristic | Dropped | Proceeded |
|----------------|---------|-----------|
| Work email | 62% | 85% |
| Company size >10 | 34% | 52% |
| Came from referral | 12% | 28% |

### Root Causes (Survey Data, n=124)

| Reason | % |
|--------|---|
| "Just exploring, not ready" | 35% |
| "Looked too complicated" | 28% |
| "Didn't understand the value" | 22% |
| "Needed team buy-in first" | 10% |
| "Technical issues" | 5% |

### Recommendations

1. **Simplify first impression** - Show value before asking for info
2. **Quick demo option** - Let users try without signup
3. **Clearer value prop** - Industry-specific messaging
4. **Re-engagement campaign** - Email sequence for drop-offs

---

## Drop-off Point #2: CRM Connection (26%)

### The CRM Connection Barrier

This is our biggest activation barrier. Users who connect CRM activate at 2.3x the rate.

### Where They Stop in CRM Flow

| Step | Completion | Drop-off |
|------|------------|----------|
| See CRM selection | 100% | - |
| Select CRM | 92% | 8% |
| Click "Connect" | 78% | 14% |
| Complete OAuth | 56% | **22%** |
| Map fields | 48% | 8% |
| Complete sync | 45% | 3% |

### OAuth Drop-off Analysis

| CRM | OAuth Completion | Issues |
|-----|------------------|--------|
| Salesforce | 52% | Admin approval needed |
| HubSpot | 68% | Best flow |
| Pipedrive | 61% | Confusing permissions |
| Zoho | 45% | Multiple steps |

### User Feedback (Support Tickets, n=342)

| Issue | Frequency |
|-------|-----------|
| "Need admin to approve" | 28% |
| "OAuth error/timeout" | 24% |
| "Don't understand permissions" | 18% |
| "CRM not supported" | 15% |
| "Don't want to connect yet" | 15% |

### Time Spent on CRM Setup

| Outcome | Avg Time |
|---------|----------|
| Completed | 18 minutes |
| Abandoned | 4.5 minutes |

**Insight**: Users who spend >5 minutes are likely to complete.

### Recommendations

1. **Allow skip** - Let users create workflows without CRM first
2. **Simplify OAuth** - Reduce permission requests
3. **Admin flow** - Dedicated flow for getting admin approval
4. **Progress saving** - Don't lose progress on errors
5. **Manual entry fallback** - CSV import as alternative

---

## Drop-off Point #3: First Workflow (7%)

### Why Users Don't Create Workflows

| Barrier | % |
|---------|---|
| "Don't know where to start" | 42% |
| "Templates don't match my needs" | 25% |
| "Workflow builder confusing" | 18% |
| "Waiting for CRM data" | 15% |

### Workflow Builder Friction Points

| Issue | Impact |
|-------|--------|
| Blank canvas intimidating | High |
| Step configuration complex | Medium |
| Unclear what each step does | Medium |
| No undo/version history | Low |

### Template Discovery

| Behavior | % of Users |
|----------|------------|
| Used template browser | 58% |
| Found relevant template | 72% of browsers |
| Actually used template | 45% of finders |

**Gap**: Users browse but don't find/use templates.

### Recommendations

1. **AI-first creation** - "Tell us what you want to automate"
2. **Industry templates** - Pre-select based on signup data
3. **Guided builder** - Step-by-step wizard option
4. **Sample data** - Show workflows working with demo data

---

## Drop-off Point #4: First Run (7%)

### Why Workflows Don't Run

| Reason | % |
|--------|---|
| Workflow saved but not activated | 45% |
| Trigger not configured | 28% |
| Waiting for trigger event | 15% |
| Technical error | 12% |

### Time from Creation to First Run

| Segment | Time | Success Rate |
|---------|------|--------------|
| Same session | <1 hour | 85% |
| Same day | 1-24 hours | 68% |
| Next day | 24-48 hours | 52% |
| Later | >48 hours | 35% |

**Insight**: If they don't run within 24 hours, likelihood drops significantly.

### Recommendations

1. **Auto-activate prompts** - Encourage immediate activation
2. **Test run feature** - Run with sample data before live
3. **Activation reminder** - Email if workflow created but not run
4. **Progress celebration** - Gamify first run completion

---

## Activation by Segment

### By Plan

| Plan | Activation Rate | Target |
|------|-----------------|--------|
| Starter | 28% | 50% |
| Professional | 38% | 60% |
| Enterprise | 42% | 70% |

### By Company Size

| Size | Activation Rate | Barrier |
|------|-----------------|---------|
| 1-10 | 32% | Value clarity |
| 11-50 | 45% | Best fit |
| 51-200 | 38% | Approval process |
| 201-500 | 28% | IT complexity |
| 500+ | 22% | Enterprise barriers |

### By Source

| Acquisition Source | Activation |
|--------------------|------------|
| Referral | 52% |
| Content/SEO | 35% |
| Paid (LinkedIn) | 28% |
| Paid (Google) | 25% |
| Trial from demo | 48% |

---

## Activation Improvement Experiments

### Planned A/B Tests

| Test | Hypothesis | Launch |
|------|------------|--------|
| Skip CRM option | +10pp activation | Feb 2026 |
| AI workflow creation | +15pp activation | Mar 2026 |
| Simplified OAuth | +8pp at CRM step | Feb 2026 |
| Industry onboarding | +5pp activation | Apr 2026 |

### Previous Learnings

| Experiment | Result | Action |
|------------|--------|--------|
| Progress bar in onboarding | +3pp | Shipped |
| Template first approach | +5pp | Shipped |
| Shorter signup form | +8pp to start | Shipped |
| CRM required removal | +12pp activation | **Recommended** |

---

## Action Plan

### Immediate (Week 1-2)

1. Add "Skip for now" to CRM connection
2. Improve OAuth error messages
3. Add workflow template recommendations

### Short-term (Q2 2026)

1. Launch AI workflow creation
2. Rebuild CRM OAuth flow
3. Add guided onboarding path
4. Implement activation email sequence

### Success Metrics

| Metric | Current | Q2 Target | Q4 Target |
|--------|---------|-----------|-----------|
| Activation Rate | 31% | 45% | 60% |
| CRM Connection | 34% | 45% | 55% |
| TTFV | 12 days | 5 days | 3 days |

---

*Report Date: January 2026*
*Owner: Activation Team*
