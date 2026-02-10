# Opportunity Solution Tree 2026

> Strategic mapping of objectives to opportunities and solutions.

## Overview

The Opportunity Solution Tree (OST) helps us maintain clear connections between business objectives, customer opportunities, and solution ideas.

---

## North Star Objective

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   NORTH STAR: Become the leading AI-powered sales automation   │
│   platform for B2B teams in EMEA by 2028                       │
│                                                                 │
│   Metric: Active Workflows Run per Month                       │
│   Current: 120K → Target 2026: 500K                            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## Objective Tree

```
                           NORTH STAR
                               │
         ┌─────────────────────┼─────────────────────┐
         │                     │                     │
         ▼                     ▼                     ▼
    ┌─────────┐          ┌─────────┐          ┌─────────┐
    │   O1    │          │   O2    │          │   O3    │
    │ Retain  │          │  Grow   │          │ Engage  │
    │Enterprise│         │Customers│          │ Users   │
    └────┬────┘          └────┬────┘          └────┬────┘
         │                    │                    │
    ┌────┴────┐          ┌────┴────┐          ┌────┴────┐
    │         │          │         │          │         │
   O1.1     O1.2       O2.1      O2.2       O3.1      O3.2
  Fix      Build      Improve   Enterprise  AI       Workflows
 Churn    Success    Activation Features  Features   Adoption
```

---

## O1: Retain Enterprise Customers

**Objective**: Reduce enterprise churn from 12.3% to <5%

### O1.1: Fix Integration Churn

**Opportunity**: 28% of enterprise churn cites integration complexity

```
O1.1 Fix Integration Churn
│
├── Opportunity: CRM setup is too complex
│   ├── Solution: Simplified OAuth flow
│   ├── Solution: Skip CRM option
│   └── Solution: White-glove setup service
│
├── Opportunity: Sync reliability issues
│   ├── Solution: CRM Sync v2 architecture
│   ├── Solution: Conflict resolution improvements
│   └── Solution: Real-time sync status
│
└── Opportunity: Missing CRM support
    ├── Solution: Microsoft Dynamics integration
    └── Solution: Universal API connector
```

### O1.2: Build Enterprise Success Program

**Opportunity**: Enterprise customers need dedicated attention

```
O1.2 Enterprise Success Program
│
├── Opportunity: No dedicated support
│   ├── Solution: 24/7 enterprise support
│   ├── Solution: Dedicated CSM assignment
│   └── Solution: QBR process
│
├── Opportunity: Missing enterprise features
│   ├── Solution: SAML SSO
│   ├── Solution: Audit logs
│   └── Solution: Advanced permissions
│
└── Opportunity: Slow issue resolution
    ├── Solution: Priority support queue
    └── Solution: Executive escalation path
```

---

## O2: Grow Customer Base

**Objective**: Grow from 1,847 to 3,000 customers

### O2.1: Improve Activation

**Opportunity**: Only 45% of signups activate

```
O2.1 Improve Activation
│
├── Opportunity: Users don't start onboarding (22% drop)
│   ├── Solution: Simplified first screen
│   ├── Solution: Quick demo mode
│   └── Solution: Value preview before signup
│
├── Opportunity: CRM connection barrier (26% drop)
│   ├── Solution: Skip CRM option
│   ├── Solution: OAuth flow redesign
│   └── Solution: CSV import alternative
│
├── Opportunity: Blank canvas problem (42% don't know where to start)
│   ├── Solution: Template-first experience
│   ├── Solution: AI workflow creation
│   └── Solution: Guided setup wizard
│
└── Opportunity: Long time to first value (12 days)
    ├── Solution: Sample data to start
    ├── Solution: Progress tracking
    └── Solution: Activation email sequence
```

### O2.2: Enterprise Market Expansion

**Opportunity**: Enterprise is highest LTV segment

```
O2.2 Enterprise Expansion
│
├── Opportunity: Security requirements not met
│   ├── Solution: SAML SSO
│   ├── Solution: SOC 2 certification
│   └── Solution: GDPR documentation
│
├── Opportunity: Long sales cycle (78 days)
│   ├── Solution: Self-serve trial for enterprise
│   ├── Solution: ROI calculator
│   └── Solution: Case studies by industry
│
└── Opportunity: Enterprise feature gaps
    ├── Solution: Advanced workflow conditions
    ├── Solution: Custom API access
    └── Solution: Multi-workspace support
```

---

## O3: Increase User Engagement

**Objective**: Increase DAU/MAU from 26% to 35%

### O3.1: AI Feature Adoption

**Opportunity**: AI users retain 14% better but only 12% adopt

```
O3.1 AI Feature Adoption
│
├── Opportunity: Low AI discoverability
│   ├── Solution: AI prompts in workflow builder
│   ├── Solution: AI onboarding path
│   └── Solution: AI feature tour
│
├── Opportunity: AI entry barrier too high
│   ├── Solution: AI workflow creation (describe to build)
│   ├── Solution: AI-powered templates
│   └── Solution: AI suggestions everywhere
│
└── Opportunity: AI value not demonstrated
    ├── Solution: Before/after comparison
    ├── Solution: AI impact metrics
    └── Solution: AI success stories
```

### O3.2: Workflow Adoption

**Opportunity**: Users create average 8 workflows but power users create 24+

```
O3.2 Workflow Adoption
│
├── Opportunity: Workflow builder friction
│   ├── Solution: Undo/redo functionality
│   ├── Solution: Workflow versioning
│   └── Solution: Better status feedback
│
├── Opportunity: Limited templates
│   ├── Solution: Industry-specific templates
│   ├── Solution: Community templates
│   └── Solution: AI-generated templates
│
└── Opportunity: Unclear workflow value
    ├── Solution: Workflow performance metrics
    ├── Solution: Time saved calculations
    └── Solution: Workflow optimization suggestions
```

---

## Solution Prioritization

### Priority Matrix

| Solution | Impact | Effort | Dependencies | Priority |
|----------|--------|--------|--------------|----------|
| CRM Sync v2 | High | High | None | P0 |
| SAML SSO | High | Medium | None | P0 |
| AI Workflow Creation | High | Medium | None | P0 |
| Skip CRM Option | Medium | Low | None | P0 |
| OAuth Flow Redesign | Medium | Low | None | P0 |
| Audit Logs | Medium | Medium | SAML | P0 |
| Template-first Experience | Medium | Medium | None | P1 |
| AI Everywhere | Medium | Medium | AI Creation | P1 |
| 24/7 Enterprise Support | High | High | Hiring | P1 |
| Mobile Optimization | Medium | High | None | P2 |

### Q2 2026 Solution Focus

```
         HIGH IMPACT
              │
    ┌─────────┼─────────┐
    │         │         │
    │  CRM    │  SAML   │
    │ Sync v2 │   SSO   │
    │         │         │
LOW ├─────────┼─────────┤ HIGH
EFF │         │         │ EFFORT
    │  Skip   │   AI    │
    │   CRM   │ Create  │
    │  OAuth  │         │
    └─────────┼─────────┘
              │
         LOW IMPACT

Focus Zone: High Impact solutions across effort spectrum
```

---

## Opportunity Validation Status

| Opportunity | Validated | Method | Confidence |
|-------------|-----------|--------|------------|
| CRM complexity | ✅ | Data + interviews | High |
| 22% pre-onboarding drop | ✅ | Analytics | High |
| Blank canvas problem | ✅ | User research | High |
| AI drives retention | ✅ | Data analysis | High |
| Enterprise feature gaps | ✅ | Customer feedback | High |
| Mobile need | ⚠️ | Requests only | Medium |
| Multi-workspace need | ⚠️ | Enterprise feedback | Medium |

---

## Next Steps

1. **Validate remaining opportunities** - Mobile, multi-workspace
2. **Prototype priority solutions** - AI workflow creation
3. **Run experiments** - Skip CRM option
4. **Track opportunity metrics** - Regular review

---

*Document Owner: Product Team*
*Last Updated: January 2026*
*Review: Monthly*
