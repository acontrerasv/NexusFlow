---
name: prd-compliance-validator
description: Validates PRD documents against NexusFlow's PRD standards, checking for completeness, quality, and consistency. Provides a compliance score and actionable feedback.
---

# PRD Compliance Validator

## Capabilities

- Validate PRD structure completeness
- Check required sections and fields
- Assess content quality
- Verify OKR alignment
- Score PRD compliance (0-100)
- Generate improvement recommendations

## Inputs

| Input | Type | Required | Description |
|-------|------|----------|-------------|
| prd_content | string | Yes | PRD markdown content to validate |
| template | enum | No | Template to validate against (full, onepage, quickwin) |
| strict | boolean | No | Strict mode fails on any missing element |

## Outputs

| Output | Type | Description |
|--------|------|-------------|
| score | number | Compliance score (0-100) |
| passed | boolean | Whether PRD passes minimum threshold |
| sections | object | Section-by-section validation |
| issues | array | List of issues found |
| recommendations | array | Improvement suggestions |

## Validation Rules

### Structure Validation

#### Full PRD Required Sections

| Section | Required | Weight | Validation |
|---------|----------|--------|------------|
| Metadata | Yes | 5% | Has author, date, status, team |
| Executive Summary | Yes | 5% | 100-300 words |
| Problem Statement | Yes | 15% | Clear problem, evidence, impact |
| User Stories | Yes | 15% | At least 3, proper format |
| Solution | Yes | 15% | Hypothesis, approach, scope |
| Requirements | Yes | 15% | Functional + non-functional |
| Success Metrics | Yes | 15% | At least 3 measurable metrics |
| Timeline | Yes | 10% | Milestones with dates |
| Risks | Yes | 5% | At least 2 risks with mitigations |

#### OnePage PRD Required Sections

| Section | Required | Weight |
|---------|----------|--------|
| Overview | Yes | 10% |
| Problem | Yes | 20% |
| Solution | Yes | 20% |
| User Stories | Yes | 15% |
| Metrics | Yes | 15% |
| Scope | Yes | 10% |
| Timeline | Yes | 10% |

#### QuickWin Spec Required Sections

| Section | Required | Weight |
|---------|----------|--------|
| ID | Yes | 5% |
| Problem | Yes | 25% |
| Solution | Yes | 25% |
| User Story | Yes | 20% |
| Acceptance Criteria | Yes | 20% |
| Success Metric | Yes | 5% |

### Content Quality Validation

| Check | Rule | Severity |
|-------|------|----------|
| Problem Evidence | Must have data or quotes | Error |
| Metrics Measurable | Must have baseline + target | Error |
| Scope Defined | Must have in-scope and out-scope | Warning |
| User Story Format | As a/I want/So that | Warning |
| Acceptance Testable | Must be verifiable | Warning |
| Timeline Realistic | Milestones have dates | Warning |
| Risks Mitigated | Each risk has mitigation | Warning |
| OKR Referenced | Links to company OKRs | Warning |

### Specific Validations

```yaml
problem_statement:
  min_length: 50
  max_length: 500
  must_contain:
    - evidence (data or quote)
    - impact statement
  must_not_contain:
    - solution language

user_story:
  format: "As a [persona], I want [action], so that [benefit]"
  must_have:
    - acceptance_criteria (min 2)
  persona_must_exist: true

metrics:
  min_count: 3
  must_have:
    - name
    - baseline (current value)
    - target (goal value)
    - method (how measured)

scope:
  must_have:
    - in_scope (min 3 items)
    - out_of_scope (min 2 items)

risks:
  min_count: 2
  must_have:
    - description
    - probability (low/medium/high)
    - impact (low/medium/high)
    - mitigation
```

## Scoring Algorithm

```python
def calculate_compliance_score(prd, template="full"):
    """
    Calculate PRD compliance score (0-100)
    """
    scores = []

    # Structure score (40%)
    structure_score = validate_structure(prd, template)
    scores.append(('structure', structure_score, 0.40))

    # Content quality score (35%)
    quality_score = validate_quality(prd)
    scores.append(('quality', quality_score, 0.35))

    # Completeness score (15%)
    completeness_score = validate_completeness(prd)
    scores.append(('completeness', completeness_score, 0.15))

    # Alignment score (10%)
    alignment_score = validate_alignment(prd)
    scores.append(('alignment', alignment_score, 0.10))

    total = sum(score * weight for _, score, weight in scores)
    return round(total)

def passes_validation(score, template):
    """Check if score passes minimum threshold"""
    thresholds = {
        'full': 75,
        'onepage': 70,
        'quickwin': 65
    }
    return score >= thresholds.get(template, 70)
```

## Output Format

### Validation Report

```markdown
# PRD Validation Report

## Summary
| Aspect | Score | Status |
|--------|-------|--------|
| **Overall** | **78/100** | **PASS** |
| Structure | 82/100 | ✅ |
| Quality | 75/100 | ✅ |
| Completeness | 80/100 | ✅ |
| Alignment | 70/100 | ⚠️ |

## Section Validation

### Problem Statement ✅
- [x] Present and well-defined
- [x] Contains evidence (data point found)
- [x] Impact clearly stated
- Score: 90/100

### User Stories ⚠️
- [x] Present (4 stories)
- [x] Proper format
- [ ] Missing acceptance criteria on US-003
- Score: 75/100

### Success Metrics ⚠️
- [x] Present (3 metrics)
- [ ] Metric 2 missing baseline
- [ ] Metric 3 missing measurement method
- Score: 65/100

## Issues Found

### Errors (Must Fix)
1. **Missing baseline for metric**: "Activation Rate" needs current value
2. **Incomplete user story**: US-003 missing acceptance criteria

### Warnings (Should Fix)
1. **Weak evidence**: Problem statement would benefit from more data
2. **Missing OKR reference**: No explicit OKR alignment documented
3. **Vague timeline**: Milestone 2 missing specific date

### Suggestions (Optional)
1. Consider adding competitive context
2. Technical architecture section recommended for this scope

## Recommendations
1. Add current activation rate (45%) as baseline for metric
2. Add 2-3 acceptance criteria to US-003
3. Reference O2-KR3 for OKR alignment
4. Specify date for "Technical Review" milestone

## Re-validation
After addressing errors, run validation again to confirm PASS status.
```

## Usage Example

```python
# Validate a PRD
result = prd_compliance_validator.validate(
    prd_content=prd_markdown,
    template="full",
    strict=False
)

# Check results
if result.passed:
    print(f"PRD passed with score: {result.score}")
else:
    print(f"PRD failed with score: {result.score}")
    for issue in result.issues:
        print(f"- [{issue.severity}] {issue.message}")
```

## Integration

| Agent | Usage |
|-------|-------|
| product-manager | Primary validator |
| ai-pm | Quality assurance |

| Command | Usage |
|---------|-------|
| /prd-writer | Validation step |

## Thresholds

| Template | Pass | Good | Excellent |
|----------|------|------|-----------|
| Full PRD | 75 | 85 | 95 |
| OnePage | 70 | 80 | 90 |
| QuickWin | 65 | 75 | 85 |

## Metadata

- **Owner**: Product Team
- **Created**: 2025-06-01
- **Updated**: 2026-01-15
