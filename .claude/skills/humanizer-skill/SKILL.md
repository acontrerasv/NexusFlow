---
name: humanizer
description: Improves the readability, clarity, and engagement of written content while maintaining professional tone. Makes technical or corporate writing more accessible and human.
---

# Humanizer

## Capabilities

- Improve readability scores
- Simplify complex language
- Add appropriate tone
- Fix passive voice
- Remove jargon
- Improve structure
- Maintain technical accuracy
- Adapt to audience

## Inputs

| Input | Type | Required | Description |
|-------|------|----------|-------------|
| content | string | Yes | Content to humanize |
| audience | enum | No | Target audience (technical, executive, general) |
| tone | enum | No | Desired tone (professional, casual, friendly) |
| preserve | string[] | No | Terms to preserve unchanged |

## Outputs

| Output | Type | Description |
|--------|------|-------------|
| humanized | string | Improved content |
| readability_before | number | Original readability score |
| readability_after | number | New readability score |
| changes | array | List of changes made |

## Humanization Rules

### Language Improvements

| Rule | Before | After |
|------|--------|-------|
| Active voice | "The report was generated" | "We generated the report" |
| Remove jargon | "Leverage synergies" | "Work together" |
| Simplify | "In order to" | "To" |
| Direct address | "Users should" | "You should" |
| Concrete words | "Facilitate" | "Help" |
| Shorter sentences | 40+ word sentences | Break into 2-3 sentences |

### Jargon Replacement

| Jargon | Plain Language |
|--------|----------------|
| Leverage | Use |
| Utilize | Use |
| Facilitate | Help, enable |
| Optimize | Improve |
| Synergy | Working together |
| Paradigm | Model, approach |
| Bandwidth | Time, capacity |
| Circle back | Follow up |
| Deep dive | Detailed look |
| Move the needle | Make progress |

### Tone Adjustments

| Original | Professional | Friendly |
|----------|--------------|----------|
| "It is required that..." | "You need to..." | "Please..." |
| "Failure to comply..." | "If you don't..." | "Make sure to..." |
| "As per the above..." | "As mentioned..." | "Like we said..." |
| "Kindly be advised..." | "Please note..." | "Just so you know..." |

## Readability Scoring

### Flesch Reading Ease

```python
def flesch_reading_ease(text):
    """
    Calculate Flesch Reading Ease score

    Score = 206.835 - 1.015(words/sentences) - 84.6(syllables/words)

    90-100: Very easy (5th grade)
    80-90: Easy (6th grade)
    70-80: Fairly easy (7th grade)
    60-70: Standard (8th-9th grade)  ← Target for general
    50-60: Fairly difficult (10th-12th)
    30-50: Difficult (college)
    0-30: Very difficult (college graduate)
    """
    words = count_words(text)
    sentences = count_sentences(text)
    syllables = count_syllables(text)

    score = 206.835 - 1.015 * (words / sentences) - 84.6 * (syllables / words)
    return round(score, 1)
```

### Target Scores by Audience

| Audience | Target Score | Reading Level |
|----------|-------------|---------------|
| General | 60-70 | 8th-9th grade |
| Technical | 50-60 | 10th-12th grade |
| Executive | 55-65 | 9th-11th grade |

## Transformation Patterns

### Before/After Examples

#### Corporate Speak → Clear Communication

**Before:**
> We are currently in the process of implementing a strategic initiative to optimize our customer engagement workflows through the utilization of artificial intelligence capabilities, which will facilitate enhanced productivity and drive significant improvements in key performance indicators.

**After:**
> We're adding AI to our customer engagement tools. This will help your team work faster and improve results.

**Changes:**
- Reduced word count: 47 → 22 (-53%)
- Readability: 18 → 62 (+44 points)
- Removed: "in the process of", "strategic initiative", "utilization", "facilitate", "key performance indicators"
- Added: Direct address ("your team")

#### Technical → Accessible

**Before:**
> The system leverages a microservices architecture with event-driven communication patterns, utilizing message queues for asynchronous processing and implementing circuit breakers for fault tolerance.

**After:**
> The system is built from small, independent services that talk to each other through messages. This design handles failures gracefully and keeps things running smoothly even when problems occur.

**Changes:**
- Split technical jargon into plain explanations
- Added "why it matters" context
- Maintained technical accuracy

### Passive to Active Voice

| Passive | Active |
|---------|--------|
| The workflow was created by the user | The user created the workflow |
| The data is processed by the system | The system processes the data |
| Errors are logged automatically | The system automatically logs errors |
| The feature was requested by customers | Customers requested this feature |

## Audience Adaptation

### General Audience
- Reading level: 8th grade
- Avoid all jargon
- Use analogies
- Short paragraphs (3-4 sentences)
- Explain acronyms

### Technical Audience
- Reading level: 10th-12th grade
- Use standard technical terms
- Precise language
- Code examples acceptable
- Acronyms OK after first use

### Executive Audience
- Reading level: 9th-11th grade
- Lead with impact/results
- Use business terms
- Bullet points for key info
- Action-oriented

## Output Format

### Humanization Report

```markdown
# Humanization Report

## Summary
| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Word Count | 347 | 198 | -43% |
| Readability | 42 | 65 | +23 |
| Passive Voice | 12 | 2 | -83% |
| Avg Sentence Length | 28 | 16 | -43% |

## Humanized Content

[Improved content here]

## Changes Made

### Language Simplification
1. "Utilize" → "Use" (4 instances)
2. "Facilitate" → "Help" (2 instances)
3. "In order to" → "To" (3 instances)

### Passive to Active
1. "was implemented" → "we implemented"
2. "is being processed" → "processes"

### Sentence Restructuring
1. Split 45-word sentence into 2 sentences
2. Reordered paragraph for clarity

### Jargon Removal
1. "Leverage synergies" → "work together"
2. "Deep dive" → "detailed look"

## Preserved Terms
- NexusFlow (brand name)
- API (technical term, audience appropriate)
- CRM (defined on first use)
```

## Usage Example

```python
# Humanize content
result = humanizer_skill.humanize(
    content=original_text,
    audience="general",
    tone="friendly",
    preserve=["NexusFlow", "API"]
)

print(f"Readability improved: {result.readability_before} → {result.readability_after}")
print(result.humanized)
```

## Integration

| Agent | Usage |
|-------|-------|
| product-manager | PRD writing |
| ai-product-marketing | Marketing copy |

## Metadata

- **Owner**: Content Team
- **Created**: 2025-09-01
- **Updated**: 2026-01-08
