# Discovery Orchestrator Command

## Command

```
/discovery-orchestrator
```

## Version
1.4.0

## Description

The Discovery Orchestrator runs a comprehensive discovery process for new features or product initiatives. It coordinates multiple agents to gather context, analyze data, research users, and synthesize findings into actionable insights.

## When to Use

- Starting work on a new feature or initiative
- Exploring a problem space before writing a PRD
- Validating assumptions about user needs
- Understanding the full context of a product decision

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `feature` | string | Yes | - | Feature name or area to explore |
| `depth` | enum | No | standard | Discovery depth: quick, standard, deep |
| `include-competitive` | boolean | No | true | Include competitive analysis |
| `include-data` | boolean | No | true | Include quantitative analysis |
| `team` | string | No | auto | Team owning the feature |

## Usage Examples

```bash
# Basic discovery
/discovery-orchestrator feature="Dashboard Redesign"

# Quick discovery without competitive analysis
/discovery-orchestrator feature="Minor UX Fix" depth=quick include-competitive=false

# Deep discovery for major initiative
/discovery-orchestrator feature="AI Workflow Templates" depth=deep
```

## Workflow

### Phase 1: Context Gathering (ai-pm)
**Duration**: ~5 minutes

1. Search existing documentation for related content
2. Identify relevant PRDs, research, and decisions
3. Map feature to OKRs and strategic priorities
4. List known constraints and dependencies

**Output**: Context Summary

### Phase 2: Quantitative Analysis (ai-data-analyst)
**Duration**: ~10 minutes

1. Pull relevant usage metrics
2. Analyze user behavior related to feature area
3. Identify trends and patterns
4. Calculate business impact potential

**Output**: Data Analysis Report

### Phase 3: Qualitative Research (ai-user-researcher)
**Duration**: ~15 minutes

1. Review existing user research
2. Identify target personas
3. Document known pain points
4. Map user journey for feature area
5. List open questions for validation

**Output**: User Research Summary

### Phase 4: Competitive Analysis (competitive-benchmarking)
**Duration**: ~10 minutes (if enabled)

1. Identify relevant competitors
2. Analyze competitor approaches
3. Document feature gaps
4. Note differentiation opportunities

**Output**: Competitive Brief

### Phase 5: Synthesis (product-manager)
**Duration**: ~10 minutes

1. Consolidate all findings
2. Identify key insights
3. Formulate problem hypotheses
4. Recommend next steps
5. Generate discovery summary document

**Output**: DISCOVERY_SUMMARY.md

## Output Format

### DISCOVERY_SUMMARY.md

```markdown
# Discovery Summary: [Feature Name]

## Metadata
- **Date**: [Date]
- **Orchestrated By**: discovery-orchestrator v1.4.0
- **Depth**: [quick/standard/deep]
- **Duration**: [X minutes]

## Executive Summary
[2-3 paragraph summary of key findings]

## Strategic Context

### OKR Alignment
| OKR | Alignment | Notes |
|-----|-----------|-------|
| [OKR] | High/Medium/Low | [Notes] |

### Strategic Priority
[How this fits into current priorities]

## Problem Space

### Problem Statement
[Synthesized problem statement]

### Evidence
- **Quantitative**: [Key data points]
- **Qualitative**: [User research insights]
- **Competitive**: [Market context]

### Impact Assessment
| Dimension | Impact | Confidence |
|-----------|--------|------------|
| Users Affected | [Number/Segment] | High/Medium/Low |
| Business Impact | [Estimated] | High/Medium/Low |
| Strategic Value | [Assessment] | High/Medium/Low |

## User Insights

### Target Personas
1. [Persona 1]: [Key insight]
2. [Persona 2]: [Key insight]

### Pain Points
1. [Pain point with evidence]
2. [Pain point with evidence]

### Jobs to Be Done
| Job | Current Solution | Gap |
|-----|------------------|-----|
| [Job] | [How solved now] | [Gap] |

## Data Insights

### Key Metrics
| Metric | Current | Benchmark | Gap |
|--------|---------|-----------|-----|
| [Metric] | [Value] | [Target] | [Delta] |

### Trends
- [Trend 1]
- [Trend 2]

## Competitive Landscape

### Competitor Approaches
| Competitor | Approach | Strength | Weakness |
|------------|----------|----------|----------|
| [Name] | [How they solve] | [+] | [-] |

### Differentiation Opportunity
[How NexusFlow can differentiate]

## Recommendations

### Recommended Path Forward
[Primary recommendation]

### Options Considered
| Option | Pros | Cons | Effort |
|--------|------|------|--------|
| [Option 1] | [+] | [-] | [Estimate] |
| [Option 2] | [+] | [-] | [Estimate] |

### Open Questions
- [ ] [Question needing validation]
- [ ] [Question needing validation]

### Suggested Next Steps
1. [Immediate action]
2. [Short-term action]
3. [Medium-term action]

## Appendix

### Sources Referenced
- [Document 1]
- [Document 2]

### Raw Data
[Link to supporting data]
```

## Depth Levels

### Quick (~15 minutes)
- Context gathering only
- Basic data pull
- Skip competitive analysis
- High-level synthesis

### Standard (~45 minutes)
- Full context gathering
- Comprehensive data analysis
- Competitive analysis
- User research review
- Detailed synthesis

### Deep (~90 minutes)
- Exhaustive context search
- Deep data analysis with cohorts
- Extensive competitive research
- User journey mapping
- Multiple hypothesis generation
- Detailed recommendations

## Integration

### Agents Used
| Agent | Phase | Mandatory |
|-------|-------|-----------|
| ai-pm | 1, 5 | Yes |
| ai-data-analyst | 2 | Yes |
| ai-user-researcher | 3 | Yes |
| competitive-benchmarking | 4 | Optional |
| product-manager | 5 | Yes |

### Skills Used
| Skill | Purpose |
|-------|---------|
| pipeline-metrics-analyzer | Sales data context |
| okr-alignment-checker | Strategic alignment |

## Error Handling

| Error | Handling |
|-------|----------|
| Missing data | Continue with available data, note gaps |
| No user research | Flag for validation, proceed with data |
| No competitive info | Skip section, note in summary |

## Success Criteria

A successful discovery should:
- [ ] Identify clear problem statement
- [ ] Provide supporting evidence (qual + quant)
- [ ] Map to strategic priorities
- [ ] Recommend clear next steps
- [ ] Flag open questions for validation

## Metadata

- **Owner**: Product Team
- **Created**: 2025-06-01
- **Updated**: 2026-01-15
