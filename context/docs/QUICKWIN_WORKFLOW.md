# Quick Win Workflow Guide

> Process for shipping small improvements rapidly at NexusFlow.

## Overview

Quick Wins are small, well-defined improvements that can be shipped in 5 days or less. They don't require full discovery or lengthy PRDs but still follow a structured process.

### Quick Win Criteria

A feature qualifies as a Quick Win if it meets ALL of these:

| Criterion | Requirement |
|-----------|-------------|
| Effort | ≤5 engineering days |
| Scope | Single, well-defined change |
| Risk | Low risk, easily reversible |
| Dependencies | Minimal cross-team dependencies |
| Clarity | Requirements are clear |

### When to Use Quick Wins

**Good for Quick Wins:**
- UI/UX improvements
- Bug fixes with clear scope
- Performance optimizations
- Copy/content changes
- Small feature enhancements
- Technical debt items

**Not Quick Wins:**
- New features (use full PRD)
- Architecture changes
- Multi-team initiatives
- Unclear requirements
- High-risk changes

---

## Quick Win Process

```
┌─────────────────────────────────────────────────────────────┐
│                    QUICK WIN WORKFLOW                        │
│                                                              │
│  Day 0          Day 1          Day 2-4        Day 5         │
│  ┌─────┐        ┌─────┐        ┌─────┐        ┌─────┐       │
│  │SPEC │───────▶│BUILD│───────▶│TEST │───────▶│SHIP │       │
│  └─────┘        └─────┘        └─────┘        └─────┘       │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Day 0: Specification (2-4 hours)

1. **Create Quick Win Spec**
   - Use template: `QW-[TEAM]-[NNN]_SPEC.md`
   - Define problem and solution
   - Write acceptance criteria
   - Get PM + Eng Lead approval

2. **Validate Scope**
   - Confirm ≤5 days effort
   - Identify any blockers
   - Check dependencies

3. **Schedule Work**
   - Add to sprint
   - Assign engineer
   - Set ship date

### Days 1-4: Build & Test

1. **Development**
   - Implement solution
   - Write tests
   - Self-review code

2. **Code Review**
   - PR review
   - Address feedback
   - Merge to staging

3. **QA**
   - Test acceptance criteria
   - Edge case verification
   - Performance check

### Day 5: Ship

1. **Final Verification**
   - Staging sign-off
   - PM approval

2. **Deploy**
   - Deploy to production
   - Monitor metrics
   - Verify success

3. **Close Out**
   - Update spec with results
   - Communicate completion
   - Add to changelog

---

## Quick Win Spec Template

```markdown
# Quick Win: [Title]

## ID: QW-[TEAM]-[NNN]

## Metadata
| Field | Value |
|-------|-------|
| Team | [activation/retention/integration/engagement/platform] |
| Owner | [PM Name] |
| Engineer | [Eng Name] |
| Effort | [X days] |
| Priority | [P0/P1/P2/P3] |
| Status | [Proposed/Approved/In Progress/Complete] |
| Created | [Date] |
| Ship Date | [Target Date] |

## Problem
[1-2 sentences describing the problem]

**Evidence:**
- [Data point or user feedback]
- [Support ticket reference if applicable]

## Solution
[1-2 sentences describing what we'll build]

## User Story
As a [persona],
I want to [action],
So that [benefit].

## Acceptance Criteria
- [ ] [Testable criterion 1]
- [ ] [Testable criterion 2]
- [ ] [Testable criterion 3]

## Technical Notes
[Any technical considerations, constraints, or approach notes]

## Out of Scope
- [Thing we're NOT doing]
- [Adjacent improvement we're deferring]

## Success Metric
[Single metric to measure success]
- Baseline: [Current value]
- Target: [Goal value]

## Risks
| Risk | Impact | Mitigation |
|------|--------|------------|
| [Risk] | L/M/H | [Mitigation] |

## Approval
- [ ] PM: [Name] - [Date]
- [ ] Eng Lead: [Name] - [Date]

---

## Implementation Log

### Day 1: [Date]
[Notes on progress]

### Day 2: [Date]
[Notes on progress]

### Shipped: [Date]
**Result:** [Success/Partial/Reverted]
**Actual Metric:** [Measured value]
**Notes:** [Any learnings]
```

---

## Quick Win Naming Convention

**Format**: `QW-[TEAM]-[NNN]`

| Team | Code |
|------|------|
| Activation | ACT |
| Retention | RET |
| Integration | INT |
| Engagement | ENG |
| Platform | PLT |

**Examples**:
- `QW-RET-001` - First retention quick win
- `QW-ACT-023` - 23rd activation quick win
- `QW-INT-007` - 7th integration quick win

---

## Quick Win Board

Track Quick Wins on a dedicated board:

| Column | Description |
|--------|-------------|
| Proposed | Awaiting approval |
| Approved | Ready for sprint |
| In Progress | Being built |
| In Review | Code review/QA |
| Shipped | Complete |
| Measuring | Awaiting metric validation |

---

## Quick Win Prioritization

### Priority Levels

| Priority | Criteria | SLA |
|----------|----------|-----|
| P0 | Urgent business need, blocking issue | Ship this week |
| P1 | High impact, clear value | Next sprint |
| P2 | Nice to have, good ROI | Backlog top |
| P3 | Low urgency | Backlog |

### Prioritization Factors

| Factor | Weight | High Score |
|--------|--------|------------|
| User Impact | 30% | Many users affected |
| Effort | 25% | Low effort |
| Strategic Fit | 25% | Aligns with OKRs |
| Risk | 20% | Low risk |

---

## Quick Win Examples

### Example 1: Dashboard Loading State
```markdown
# QW-ACT-015: Add skeleton loading to dashboard

**Problem**: Users see a blank screen for 2-3 seconds while dashboard loads.

**Solution**: Add skeleton loading states to dashboard components.

**Acceptance Criteria**:
- [ ] Skeleton appears within 100ms
- [ ] Matches layout of actual content
- [ ] Smooth transition to real content

**Effort**: 2 days
**Metric**: Reduce perceived load time by 50%
```

### Example 2: CRM Sync Error Message
```markdown
# QW-INT-042: Improve CRM sync error messages

**Problem**: When CRM sync fails, users see "Sync failed" with no guidance.

**Solution**: Show specific error message with suggested action.

**Acceptance Criteria**:
- [ ] Error messages are specific to failure type
- [ ] Each error has a suggested action
- [ ] Link to help doc included

**Effort**: 3 days
**Metric**: Reduce sync-related support tickets by 30%
```

### Example 3: Workflow Template Preview
```markdown
# QW-ENG-028: Add preview to workflow templates

**Problem**: Users can't see what a template does before applying it.

**Solution**: Add preview modal showing template steps.

**Acceptance Criteria**:
- [ ] Preview modal shows all steps
- [ ] Steps show configuration summary
- [ ] "Use Template" button in modal

**Effort**: 4 days
**Metric**: Increase template usage by 20%
```

---

## Common Quick Win Categories

### UX Improvements
- Loading states
- Error messages
- Empty states
- Microcopy updates
- Accessibility fixes

### Performance
- Query optimization
- Caching improvements
- Asset optimization
- Lazy loading

### Polish
- Animation smoothing
- Visual alignment
- Consistency fixes
- Mobile responsiveness

### Developer Experience
- Logging improvements
- Debug tooling
- Documentation updates
- Test coverage

---

## Approval Process

### PM Approval
PM reviews:
- Problem validity
- Solution appropriateness
- Priority accuracy
- Metric definition

### Eng Lead Approval
Eng Lead reviews:
- Technical feasibility
- Effort accuracy
- Risk assessment
- Resource availability

### Escalation
If PM and Eng Lead disagree:
- Escalate to team lead
- Resolution within 1 day
- Default to PM decision for product, Eng for technical

---

## Measuring Quick Wins

### During Implementation
- Track actual effort vs estimate
- Note blockers encountered
- Document scope changes

### After Ship
- Measure success metric
- Compare to baseline
- Document learnings

### Quarterly Review
- Win rate (shipped on time)
- Accuracy (estimate vs actual)
- Impact (metrics moved)

---

*Last Updated: January 2026*
*Template: `context/templates/PRD/QuickWin_Spec.md`*
