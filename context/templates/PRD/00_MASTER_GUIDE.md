# PRD System Master Guide

> Complete guide to the NexusFlow product requirements documentation system.

## Overview

The PRD system provides a structured approach to documenting product features from problem discovery through implementation. It ensures consistency, traceability, and quality across all product development.

---

## Document Types

### Full Discovery Process

For features requiring **2+ weeks** of development:

| Phase | Document | Purpose |
|-------|----------|---------|
| 1 | Problem Brief | Define and validate the problem |
| 2 | JTBD Analysis | Understand user motivations |
| 3 | Solution Hypothesis | Propose and validate solutions |
| 4 | PRD | Full requirements specification |

### Abbreviated Process

For features requiring **<2 weeks** of development:

| Document | Use Case |
|----------|----------|
| OnePage PRD | Small features with clear requirements |
| QuickWin Spec | Bug fixes, small improvements (<5 days) |

---

## When to Use Each Template

```
                    Is development >2 weeks?
                           │
              ┌────────────┴────────────┐
              │                         │
             YES                        NO
              │                         │
              ▼                         ▼
    Full Discovery Process      Is it well understood?
    (Problem → JTBD →              │
     Hypothesis → PRD)    ┌────────┴────────┐
                          │                 │
                         YES                NO
                          │                 │
                          ▼                 ▼
                    Development        OnePage PRD
                      <5 days?              │
                          │                 │
                 ┌────────┴────────┐        │
                 │                 │        │
                YES               NO        │
                 │                 │        │
                 ▼                 ▼        ▼
           QuickWin Spec    OnePage PRD  Research
                                         First
```

---

## File Organization

### Directory Structure

```
context/prds/
├── 2025/
│   ├── q3/
│   │   └── team-name/
│   │       └── feature-name/
│   │           ├── 00_FEATURE_BRIEF.md
│   │           ├── 01_Problem_Brief.md
│   │           ├── 02_JTBD.md
│   │           ├── 03_Solution_Hypothesis.md
│   │           └── 04_PRD.md
│   └── q4/
│       └── ...
└── 2026/
    └── q1/
        └── ...
```

### Naming Conventions

| Type | Pattern | Example |
|------|---------|---------|
| Full PRD | `04_PRD.md` | `04_PRD.md` |
| OnePage PRD | `PRD-{TEAM}-{ID}.md` | `PRD-ACT-042.md` |
| QuickWin | `QW-{TEAM}-{ID}_SPEC.md` | `QW-RET-001_SPEC.md` |

---

## Templates Available

| Template | File | Use Case |
|----------|------|----------|
| Problem Brief | `01_Problem_Brief_Template.md` | Problem definition |
| JTBD | `02_JTBD_Template.md` | User motivation analysis |
| Solution Hypothesis | `03_Solution_Hypothesis_Template.md` | Solution validation |
| Full PRD | `PRD_Template.md` | Complete requirements |
| OnePage PRD | `PRD_Template_OnePage.md` | Small features |
| QuickWin Spec | `QuickWin_Spec.md` | Bug fixes, improvements |
| Validation Checklist | `PRD_Validation_Checklist.md` | Quality assurance |

---

## Process Flow

### Full Discovery

```
Week 1: Problem Brief
├── Define problem statement
├── Gather evidence
├── Analyze root causes
└── Get PM approval

Week 2: JTBD Analysis
├── Map user jobs
├── Identify emotional jobs
├── Score opportunities
└── Get stakeholder review

Week 3: Solution Hypothesis
├── Define hypothesis
├── Propose solutions
├── Plan validation
└── Get design review

Week 4+: PRD
├── Write requirements
├── Define success criteria
├── Plan launch
└── Get final approval
```

### QuickWin Process

```
Day 1: Spec
├── Define scope
├── Write requirements
├── Get PM approval
└── Start development

Day 2-5: Development
├── Implement
├── Test
└── Ship
```

---

## Quality Standards

### Problem Brief

- [ ] Clear problem statement
- [ ] Quantified impact
- [ ] Evidence from data/research
- [ ] Root cause analysis
- [ ] Success criteria defined

### JTBD Analysis

- [ ] Core job statement complete
- [ ] Functional jobs identified
- [ ] Emotional jobs identified
- [ ] Competing solutions analyzed
- [ ] Opportunity scores calculated

### Solution Hypothesis

- [ ] Hypothesis clearly stated
- [ ] Solutions mapped to problems
- [ ] Validation plan defined
- [ ] Risks identified
- [ ] Go/no-go criteria set

### PRD

- [ ] Goals and non-goals defined
- [ ] User stories complete
- [ ] Functional requirements listed
- [ ] Technical requirements listed
- [ ] Success metrics defined
- [ ] Launch plan included

---

## Review Process

### Review Gates

| Document | Reviewers | Approval |
|----------|-----------|----------|
| Problem Brief | PM Lead, Design | PM Lead |
| JTBD | PM Lead, Research | PM Lead |
| Solution Hypothesis | PM Lead, Eng Lead, Design | PM Lead |
| PRD | PM Lead, Eng Lead, QA | CPO |

### Review Checklist

1. **Completeness** - All required sections filled
2. **Clarity** - Requirements unambiguous
3. **Feasibility** - Engineering confirms achievable
4. **Alignment** - Maps to OKRs and roadmap
5. **Quality** - Follows template standards

---

## Tools Integration

### Jira Integration

PRDs link to Jira epics:
```
PRD-ACT-001 → JIRA: ACT-123
```

### Figma Integration

Design links in PRDs:
```markdown
### Designs
- [Wireframes](https://figma.com/...)
- [Final Designs](https://figma.com/...)
```

### Analytics Integration

Metrics link to dashboards:
```markdown
### Success Metrics
- [Dashboard](https://analytics.nexusflow.io/...)
```

---

## Common Mistakes

### Problem Brief

❌ **Vague problem**: "Users don't like the dashboard"
✅ **Specific problem**: "34% of users bounce from dashboard within 10 seconds because they don't know what action to take"

### JTBD

❌ **Feature-focused**: "Users want a search box"
✅ **Job-focused**: "Users want to quickly find specific contacts without browsing lists"

### PRD

❌ **Implementation details**: "Use React with Redux"
✅ **Requirements**: "Page must load within 1 second"

---

## FAQ

### When do I need a full PRD vs OnePage?

**Full PRD** when:
- Feature takes >2 weeks
- Multiple teams involved
- High risk or complexity
- Significant user impact

**OnePage PRD** when:
- Feature takes 1-2 weeks
- Single team
- Clear, well-understood scope
- Lower risk

### Who writes PRDs?

Product Managers own PRDs. They may collaborate with:
- Design (UX requirements)
- Engineering (technical requirements)
- Research (user insights)
- Data (metrics)

### How often should PRDs be updated?

- **During development**: As requirements change
- **After launch**: Add results section
- **Quarterly**: Archive completed PRDs

---

## Getting Started

1. Read [GETTING_STARTED.md](./GETTING_STARTED.md)
2. Choose appropriate template
3. Fill in sections
4. Submit for review
5. Iterate based on feedback
6. Get approval
7. Begin development

---

*Document Owner: Product Team*
*Last Updated: January 2026*
