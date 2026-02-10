# PRD: Smart Onboarding

> Full product requirements document for the Smart Onboarding feature.

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | PRD-ACT-001 |
| **Feature Name** | Smart Onboarding |
| **Team** | Activation |
| **PM** | Sofia Martinez |
| **Engineering Lead** | Marcus Berg |
| **Design Lead** | Elena Kowalski |
| **Status** | Shipped |
| **Version** | 1.2 |
| **Last Updated** | December 2025 |

---

## 1. Executive Summary

### Overview
Smart Onboarding transforms NexusFlow's new user experience from a one-size-fits-all flow into an AI-guided, personalized journey that reduces time to first value from 12 days to 3 days.

### Business Case
- **Problem**: 45% activation rate, 12-day TTFV
- **Solution**: Personalized, AI-guided onboarding with multiple success paths
- **Impact**: +€892K annual revenue opportunity from improved activation
- **Investment**: €85,000 (8-week sprint)
- **ROI**: 10x in first year

### Key Metrics

| Metric | Before | Target | Actual |
|--------|--------|--------|--------|
| Activation Rate | 45% | 65% | 52% |
| TTFV | 12 days | 3 days | 4.2 days |
| Onboarding Completion | 34% | 70% | 68% |

---

## 2. Problem Statement

New NexusFlow users take an average of 12 days to reach first value, with only 45% activating within 30 days. This is caused by:

1. **Generic experience** - Same flow regardless of role or goals
2. **CRM connection barrier** - 42% drop-off at OAuth step
3. **Blank canvas problem** - Users don't know where to start
4. **No value preview** - Can't try before committing

See [Problem Brief](./01_Problem_Brief.md) for full analysis.

---

## 3. Goals and Non-Goals

### Goals

1. Reduce time to first value from 12 days to 3 days
2. Increase activation rate from 45% to 65%
3. Increase onboarding completion from 34% to 70%
4. Improve onboarding satisfaction from 3.2 to 4.5/5

### Non-Goals

1. Changing the core product complexity
2. Building a fully automated onboarding bot
3. Replacing enterprise white-glove onboarding
4. Redesigning the entire dashboard

---

## 4. User Stories

### Epic: As a new user, I want to quickly understand how NexusFlow helps my specific situation

#### US-1: Role Selection
**As a** new user signing up
**I want to** select my role (Sales Rep, Manager, Ops, Executive)
**So that** I see relevant content and templates

**Acceptance Criteria**:
- [ ] Role selection appears after email verification
- [ ] 4 role options with descriptions
- [ ] Selection persists to user profile
- [ ] Dashboard customizes based on role

#### US-2: AI Goal Setting
**As a** new user during onboarding
**I want to** describe my goals in natural language
**So that** NexusFlow recommends relevant workflows

**Acceptance Criteria**:
- [ ] AI wizard asks 3-4 questions about goals
- [ ] AI suggests top 3 template workflows
- [ ] User can accept, modify, or skip suggestions
- [ ] Goals stored for future personalization

#### US-3: Skip CRM
**As a** new user without CRM access
**I want to** skip the CRM connection step
**So that** I can explore the product without blockers

**Acceptance Criteria**:
- [ ] "Skip for now" button on CRM connection step
- [ ] Clear message about what will be limited
- [ ] Sample data option offered when skipping
- [ ] Prompt to connect CRM at value moments

#### US-4: Progress Tracking
**As a** new user going through onboarding
**I want to** see my progress and time remaining
**So that** I know what to expect

**Acceptance Criteria**:
- [ ] Progress bar showing steps completed
- [ ] Time estimate for remaining steps
- [ ] Checklist of pending items
- [ ] "Resume" capability for returning users

#### US-5: Sample Data Mode
**As a** new user evaluating NexusFlow
**I want to** explore with pre-populated data
**So that** I can understand value before setup

**Acceptance Criteria**:
- [ ] Sample workspace with realistic data
- [ ] 3 working example workflows
- [ ] Clear "sample data" indicators
- [ ] Easy switch to real data

---

## 5. Functional Requirements

### 5.1 Role Selection

| Req ID | Requirement | Priority |
|--------|-------------|----------|
| FR-1.1 | System shall display role selection after email verification | P0 |
| FR-1.2 | System shall offer 4 roles: Sales Rep, Manager, Ops, Executive | P0 |
| FR-1.3 | System shall store role in user profile | P0 |
| FR-1.4 | System shall customize dashboard based on role | P0 |
| FR-1.5 | System shall allow role change in settings | P1 |

### 5.2 AI Goal Setting

| Req ID | Requirement | Priority |
|--------|-------------|----------|
| FR-2.1 | System shall present AI goal wizard after role selection | P0 |
| FR-2.2 | AI shall ask 3-4 questions about user goals | P0 |
| FR-2.3 | AI shall suggest top 3 templates based on answers | P0 |
| FR-2.4 | System shall allow user to skip goal setting | P1 |
| FR-2.5 | System shall store goals for future recommendations | P1 |

### 5.3 Skip CRM Option

| Req ID | Requirement | Priority |
|--------|-------------|----------|
| FR-3.1 | System shall display "Skip for now" on CRM step | P0 |
| FR-3.2 | System shall explain limitations when skipping | P0 |
| FR-3.3 | System shall offer sample data when CRM skipped | P0 |
| FR-3.4 | System shall prompt CRM connection at value moments | P0 |
| FR-3.5 | System shall track users who skipped for analytics | P1 |

### 5.4 Progress Tracking

| Req ID | Requirement | Priority |
|--------|-------------|----------|
| FR-4.1 | System shall display progress bar during onboarding | P0 |
| FR-4.2 | System shall show time estimate per step | P1 |
| FR-4.3 | System shall show checklist of remaining items | P0 |
| FR-4.4 | System shall remember progress for returning users | P0 |
| FR-4.5 | System shall send reminder emails for incomplete onboarding | P1 |

### 5.5 Sample Data Mode

| Req ID | Requirement | Priority |
|--------|-------------|----------|
| FR-5.1 | System shall generate sample workspace with realistic data | P0 |
| FR-5.2 | Sample workspace shall include 3 working workflows | P0 |
| FR-5.3 | System shall display "sample data" indicators | P0 |
| FR-5.4 | System shall allow switching from sample to real data | P0 |
| FR-5.5 | System shall preserve settings when switching | P1 |

---

## 6. Technical Requirements

### 6.1 Performance

| Req ID | Requirement |
|--------|-------------|
| TR-1.1 | Role selection shall load within 500ms |
| TR-1.2 | AI goal responses shall return within 3 seconds |
| TR-1.3 | Sample data generation shall complete within 5 seconds |
| TR-1.4 | Progress state shall persist across sessions |

### 6.2 Security

| Req ID | Requirement |
|--------|-------------|
| TR-2.1 | Sample data shall not include real customer information |
| TR-2.2 | AI goal inputs shall be anonymized before processing |
| TR-2.3 | Role selection shall not expose other user roles |

### 6.3 Integration

| Req ID | Requirement |
|--------|-------------|
| TR-3.1 | Integrate with existing authentication system |
| TR-3.2 | Integrate with AI Service for goal processing |
| TR-3.3 | Integrate with Analytics for event tracking |
| TR-3.4 | Integrate with CRM service for skip/connect flow |

---

## 7. UX Requirements

### 7.1 Design Principles

1. **Progressive disclosure** - Show complexity only when needed
2. **Celebrate progress** - Acknowledge every step completed
3. **Multiple paths** - Never block on a single step
4. **Consistent feedback** - Clear success/error states

### 7.2 Key Screens

1. **Role Selection** - Card-based selection with descriptions
2. **Goal Wizard** - Conversational AI interface, 3-4 questions
3. **CRM Connection** - OAuth flow with prominent skip option
4. **Progress Dashboard** - Checklist with progress bar
5. **Sample Workspace** - Full product with sample indicators

### 7.3 Responsive Requirements

| Device | Requirement |
|--------|-------------|
| Desktop | Full experience, side-by-side panels |
| Tablet | Full experience, stacked layout |
| Mobile | Simplified flow, essential steps only |

---

## 8. Analytics Requirements

### 8.1 Events to Track

| Event | Properties |
|-------|------------|
| `onboarding_started` | user_id, source, timestamp |
| `role_selected` | user_id, role, timestamp |
| `goal_wizard_started` | user_id, timestamp |
| `goal_wizard_completed` | user_id, goals[], templates_suggested[] |
| `crm_skipped` | user_id, timestamp |
| `crm_connected` | user_id, crm_type, timestamp |
| `sample_data_activated` | user_id, timestamp |
| `onboarding_completed` | user_id, duration, steps_completed |

### 8.2 Dashboards

1. **Onboarding Funnel** - Step-by-step completion rates
2. **Role Distribution** - Breakdown of user roles
3. **Skip Rate Analysis** - CRM skip rates and outcomes
4. **TTFV Tracking** - Time to first value by cohort

---

## 9. Launch Plan

### Phase 1: Beta (November 15, 2025)
- 5% of new signups
- Monitor completion rates
- Collect feedback

### Phase 2: Gradual Rollout (November 22-29)
- 25% → 50% → 75% of new signups
- A/B test against current experience
- Monitor guardrail metrics

### Phase 3: GA (December 1, 2025)
- 100% of new signups
- Deprecate old onboarding flow
- Marketing announcement

---

## 10. Success Criteria

### Launch Criteria

| Metric | Threshold | Status |
|--------|-----------|--------|
| Onboarding completion rate | ≥60% | ✅ 68% |
| TTFV (beta users) | ≤5 days | ✅ 4.2 days |
| Critical bugs | 0 | ✅ 0 |
| Performance (p95) | ≤3s | ✅ 2.1s |

### 30-Day Success Criteria

| Metric | Target | Actual |
|--------|--------|--------|
| Activation rate | 65% | 52% ⚠️ |
| TTFV | 3 days | 4.2 days ⚠️ |
| Onboarding NPS | 4.5/5 | 4.3/5 ✅ |

---

## 11. Open Questions

| Question | Owner | Status |
|----------|-------|--------|
| Should we offer different sample datasets by industry? | PM | Deferred to v1.1 |
| How long should sample data be available? | PM | 14 days, then prompt |
| Should goal setting be mandatory? | PM | No, allow skip |

---

## 12. Appendix

### A. Wireframes
[Link to Figma]

### B. User Research
- [Problem Brief](./01_Problem_Brief.md)
- [JTBD Analysis](./02_JTBD.md)
- [Solution Hypothesis](./03_Solution_Hypothesis.md)

### C. Technical Design
[Link to Technical Spec]

---

*Document Owner: Sofia Martinez*
*Last Updated: December 2025*
*Review: Post-launch retrospective completed*
