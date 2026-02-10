# PRD Writer Command

## Command

```
/prd-writer
```

## Version
2.1.0

## Description

The PRD Writer command assists in creating product requirements documents following NexusFlow's PRD framework. It guides you through the process, validates content, and ensures completeness.

## When to Use

- Starting a new PRD for a feature
- Converting discovery findings into requirements
- Reviewing and improving existing PRDs
- Creating Quick Win specifications

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `feature` | string | Yes | - | Feature name |
| `type` | enum | No | auto | full, onepage, quickwin |
| `team` | string | No | - | Owning team |
| `discovery` | string | No | - | Path to discovery summary |
| `mode` | enum | No | guided | guided, draft, review |

## Usage Examples

```bash
# Guided PRD writing
/prd-writer feature="Dashboard Redesign"

# Quick Win specification
/prd-writer feature="Fix CRM sync timeout" type=quickwin team=integration

# From discovery
/prd-writer feature="AI Templates" discovery="context/prds/2026/q2/engagement-team/ai-templates/DISCOVERY_SUMMARY.md"

# Review existing PRD
/prd-writer feature="Smart Onboarding" mode=review
```

## PRD Types

### Full PRD (>2 weeks development)
Complete documentation suite:
1. `00_FEATURE_BRIEF.md` - Executive summary
2. `01_Problem_Brief.md` - Problem definition
3. `02_JTBD.md` - Jobs to be done
4. `03_Solution_Hypothesis.md` - Proposed solution
5. `04_PRD.md` - Full requirements

### OnePage PRD (1-2 weeks)
Single consolidated document covering all essential elements.

### QuickWin Spec (<5 days)
Lightweight specification for small improvements:
- `QW-[TEAM]-[NNN]_SPEC.md`

## Workflow Modes

### Guided Mode (Default)
Interactive step-by-step process:

```
Step 1: Context Gathering
├── What problem are we solving?
├── Who is affected?
├── What's the impact?
└── What's the strategic alignment?

Step 2: Problem Definition
├── Problem statement
├── Evidence collection
├── Current state
└── Desired state

Step 3: Solution Design
├── Solution hypothesis
├── User stories
├── Scope definition
└── Success metrics

Step 4: Requirements
├── Functional requirements
├── Non-functional requirements
├── Technical considerations
└── Dependencies

Step 5: Planning
├── Timeline
├── Milestones
├── Risks
└── Launch plan

Step 6: Validation
├── Completeness check
├── OKR alignment
├── Technical review
└── Stakeholder review
```

### Draft Mode
Generate complete first draft based on inputs, minimal interaction.

### Review Mode
Analyze existing PRD, identify gaps, suggest improvements.

## Output Structure

### Full PRD Suite

```
context/prds/2026/q2/[team]/[feature]/
├── 00_FEATURE_BRIEF.md
├── 01_Problem_Brief.md
├── 02_JTBD.md
├── 03_Solution_Hypothesis.md
└── 04_PRD.md
```

### Feature Brief Template (00)

```markdown
# Feature Brief: [Feature Name]

## Metadata
| Field | Value |
|-------|-------|
| Team | [Team] |
| PM | [Name] |
| Target Release | [Quarter] |
| Status | Draft |
| PRD Link | [Link to 04_PRD.md] |

## One-Liner
[Single sentence describing the feature]

## Problem
[2-3 sentences on the problem]

## Solution
[2-3 sentences on the solution]

## Success Metrics
| Metric | Baseline | Target |
|--------|----------|--------|
| [Metric 1] | [Current] | [Goal] |
| [Metric 2] | [Current] | [Goal] |

## OKR Alignment
[Which OKRs this supports]

## Key Dates
| Milestone | Date |
|-----------|------|
| Discovery Complete | [Date] |
| PRD Approved | [Date] |
| Development Start | [Date] |
| Beta | [Date] |
| GA | [Date] |

## Quick Links
- [Problem Brief](01_Problem_Brief.md)
- [JTBD](02_JTBD.md)
- [Solution Hypothesis](03_Solution_Hypothesis.md)
- [Full PRD](04_PRD.md)
```

### QuickWin Spec Template

```markdown
# Quick Win: [Title]

## ID: QW-[TEAM]-[NNN]

## Metadata
| Field | Value |
|-------|-------|
| Team | [Team] |
| Owner | [Name] |
| Effort | [X days] |
| Priority | [P0-P3] |
| Status | Proposed |

## Problem
[1-2 sentences]

## Solution
[1-2 sentences]

## User Story
As a [persona], I want to [action], so that [benefit].

## Acceptance Criteria
- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] [Criterion 3]

## Technical Notes
[Any technical considerations]

## Success Metric
[Single metric to measure success]

## Risks
| Risk | Mitigation |
|------|------------|
| [Risk] | [Mitigation] |

## Approval
- [ ] PM: [Name]
- [ ] Eng Lead: [Name]
```

## Validation

### Completeness Checks

| Section | Required Fields | Weight |
|---------|-----------------|--------|
| Problem | Statement, Evidence, Impact | 25% |
| Solution | Hypothesis, Scope, Approach | 25% |
| Requirements | User Stories, AC, NFRs | 30% |
| Planning | Metrics, Timeline, Risks | 20% |

### Quality Criteria

- [ ] Problem is clearly stated with evidence
- [ ] Solution addresses the problem
- [ ] User stories are complete (persona, action, benefit)
- [ ] Acceptance criteria are testable
- [ ] Success metrics are measurable
- [ ] Scope is explicitly defined (in/out)
- [ ] Risks are identified with mitigations
- [ ] OKR alignment is documented
- [ ] Timeline is realistic
- [ ] Dependencies are listed

## Skills Used

| Skill | Purpose |
|-------|---------|
| prd-compliance-validator | Validate PRD completeness |
| okr-alignment-checker | Verify strategic alignment |
| business-case-calculator | Calculate business impact |

## Integration

### From Discovery
```bash
# If discovery exists, pull insights
/prd-writer feature="X" discovery="path/to/DISCOVERY_SUMMARY.md"
```

### To Development
```
PRD Approved → Jira Epic Created → Stories Generated
```

## Error Handling

| Issue | Resolution |
|-------|------------|
| Missing discovery | Prompt for problem context |
| No OKR alignment | Warn but allow proceed |
| Incomplete sections | Block until addressed |
| Missing metrics | Suggest metrics based on feature type |

## Best Practices

1. **Start with the problem** - Don't jump to solutions
2. **Get evidence** - Data or user quotes required
3. **Be specific** - Vague requirements cause rework
4. **Define scope early** - What's NOT included is as important
5. **Measurable metrics** - If you can't measure it, rethink it
6. **Review with engineering** - Technical feasibility matters

## Metadata

- **Owner**: Product Team
- **Created**: 2025-05-15
- **Updated**: 2026-01-12
