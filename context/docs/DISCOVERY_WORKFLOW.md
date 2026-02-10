# Discovery Workflow Guide

> Step-by-step guide for running product discovery at NexusFlow.

## Overview

Discovery is the process of understanding a problem space before committing to solutions. It ensures we build the right things by validating assumptions with evidence.

### When to Run Discovery

- **New Feature Development** - Before writing a PRD
- **Problem Exploration** - Understanding user pain points
- **Opportunity Assessment** - Evaluating new ideas
- **Strategic Initiatives** - Major product changes

### Discovery Depth Levels

| Level | Duration | When to Use |
|-------|----------|-------------|
| Quick | 1-2 days | Small features, clear problem |
| Standard | 1-2 weeks | Medium features, some unknowns |
| Deep | 2-4 weeks | Major initiatives, high uncertainty |

---

## Discovery Process

### Phase 1: Frame the Opportunity

**Goal**: Clearly define what we're exploring and why.

**Activities**:
1. Write an opportunity statement
2. Identify target users
3. Map to company objectives
4. Define success criteria

**Template: Opportunity Statement**
```markdown
## Opportunity: [Name]

### Statement
We believe that [target users] are struggling with [problem]
because [root cause]. If we [solve this], we expect [outcome].

### Strategic Alignment
- OKR: [Related OKR]
- Priority: [P0/P1/P2]

### Target Users
- Primary: [Persona]
- Secondary: [Persona]

### Success Criteria
- [ ] Problem validated with X users
- [ ] Impact quantified
- [ ] Solution hypothesis formed
```

**Output**: Opportunity Brief (1 page)

---

### Phase 2: Gather Context

**Goal**: Understand what we already know.

**Activities**:
1. Review existing documentation
2. Pull relevant metrics
3. Analyze support tickets
4. Check competitor approaches

**Data Sources**:
| Source | What to Look For |
|--------|------------------|
| Analytics | Usage patterns, drop-offs |
| Support Tickets | Common complaints |
| User Feedback | Feature requests, NPS comments |
| Sales Calls | Prospect objections |
| Churn Reasons | Why customers leave |

**Output**: Context Summary

---

### Phase 3: User Research

**Goal**: Validate problem and understand user needs.

**Research Methods**:

| Method | Best For | Sample Size |
|--------|----------|-------------|
| User Interviews | Deep understanding | 5-10 users |
| Surveys | Validation at scale | 50-200 users |
| Usability Tests | Evaluating solutions | 5-8 users |
| Contextual Inquiry | Understanding workflows | 3-5 users |

**Interview Guide Structure**:
1. **Warm-up** (5 min) - Build rapport
2. **Current State** (15 min) - How they work today
3. **Pain Points** (15 min) - Problems and frustrations
4. **Ideal State** (10 min) - What would better look like
5. **Wrap-up** (5 min) - Final thoughts

**Key Questions**:
- "Walk me through how you [task] today"
- "What's the most frustrating part?"
- "How do you currently work around this?"
- "What would change if this was solved?"

**Output**: User Research Summary

---

### Phase 4: Data Analysis

**Goal**: Quantify the opportunity with data.

**Key Questions**:
- How many users are affected?
- What's the current behavior?
- What's the business impact?
- How does this correlate with retention?

**Metrics to Analyze**:
| Metric | Question |
|--------|----------|
| Feature adoption | How many use related features? |
| Drop-off rates | Where do users struggle? |
| Time on task | How long does this take? |
| Support volume | How many tickets about this? |
| Churn correlation | Do affected users churn more? |

**Output**: Data Analysis Report

---

### Phase 5: Competitive Analysis

**Goal**: Understand how others solve this problem.

**Activities**:
1. Identify relevant competitors
2. Analyze their approaches
3. Document feature gaps
4. Note differentiation opportunities

**Analysis Framework**:
| Competitor | Approach | Strengths | Weaknesses | Learnings |
|------------|----------|-----------|------------|-----------|
| Competitor A | | | | |
| Competitor B | | | | |
| Workaround | | | | |

**Output**: Competitive Brief

---

### Phase 6: Synthesis

**Goal**: Consolidate findings into actionable insights.

**Activities**:
1. Identify patterns across sources
2. Validate/invalidate hypotheses
3. Size the opportunity
4. Form solution hypotheses
5. Recommend next steps

**Synthesis Questions**:
- What problem are we actually solving?
- Who has this problem most acutely?
- How big is the opportunity?
- What would success look like?
- What are the biggest risks?

**Output**: Discovery Summary

---

## Discovery Summary Template

```markdown
# Discovery Summary: [Feature/Opportunity Name]

## Executive Summary
[2-3 paragraph overview of findings]

## Opportunity Definition

### Problem Statement
[Clear, evidence-backed problem statement]

### Target Users
| Persona | Pain Intensity | Size |
|---------|---------------|------|
| [Persona 1] | High/Med/Low | X users |

### Impact Assessment
- **Users Affected**: [Number/percentage]
- **Business Impact**: [Revenue/retention/efficiency]
- **Strategic Alignment**: [OKR reference]

## Evidence

### Quantitative Findings
| Finding | Data Point | Source |
|---------|------------|--------|
| [Finding 1] | [Metric] | [Source] |

### Qualitative Findings
| Theme | Evidence | Frequency |
|-------|----------|-----------|
| [Theme 1] | "[Quote]" | X/Y users |

### Competitive Context
[Summary of how competitors address this]

## Solution Hypotheses

### Hypothesis 1: [Name]
**Approach**: [Description]
**Confidence**: High/Medium/Low
**Effort**: [Estimate]
**Expected Impact**: [Metric improvement]

### Hypothesis 2: [Name]
...

## Risks & Open Questions

### Risks
| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| [Risk 1] | H/M/L | H/M/L | [Mitigation] |

### Open Questions
- [ ] [Question requiring validation]

## Recommendations

### Recommended Path
[Primary recommendation with rationale]

### Next Steps
1. [ ] [Immediate action]
2. [ ] [Short-term action]
3. [ ] [If proceeding, next action]

## Appendix
- [Link to research notes]
- [Link to data analysis]
- [Link to competitive docs]
```

---

## Quick Discovery Checklist

### Before Starting
- [ ] Opportunity clearly defined
- [ ] Stakeholders aligned
- [ ] Resources allocated
- [ ] Timeline set

### During Discovery
- [ ] Existing docs reviewed
- [ ] Relevant metrics pulled
- [ ] 5+ user interviews conducted
- [ ] Competitive landscape analyzed
- [ ] Data quantifies impact

### Before Concluding
- [ ] Key insights documented
- [ ] Hypotheses formed
- [ ] Risks identified
- [ ] Recommendations clear
- [ ] Next steps defined

---

## Tools & Resources

### AI Assistance

| Task | Command/Agent |
|------|---------------|
| Run full discovery | `/discovery-orchestrator` |
| User research | `ai-user-researcher` |
| Data analysis | `ai-data-analyst` |
| Competitive analysis | `competitive-benchmarking` |
| Write summary | `product-manager` |

### Templates

- Opportunity Brief: `context/templates/PRD/01_Problem_Brief_Template.md`
- Interview Guide: See `ai-user-researcher` agent
- JTBD Framework: `context/templates/PRD/02_JTBD_Template.md`

---

## Examples

### Example: CRM Sync Improvements Discovery

**Duration**: 2 weeks (Standard)

**Findings**:
- 28% of enterprise churn cites integration issues
- Average CRM setup time: 4.5 hours (target: 1 hour)
- 67% of users don't complete bi-directional sync
- Competitors average 2 hours setup

**Recommendation**: Proceed with CRM Sync v2 PRD

---

*Last Updated: January 2026*
*Use `/discovery-orchestrator` for AI-assisted discovery*
