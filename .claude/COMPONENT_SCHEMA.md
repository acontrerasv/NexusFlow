# Component Schema Definitions

This document defines the schema and structure for all AI components in the NexusFlow repository.

---

## Agent Schema

### Required Fields

```yaml
agent:
  id: string                    # Unique identifier (kebab-case)
  name: string                  # Human-readable name
  description: string           # Brief description (1-2 sentences)
  version: string               # Semantic version (e.g., "1.2.0")
  role: string                  # Primary role/function

  capabilities:
    - string                    # List of capabilities

  context:
    required:
      - string                  # Required context files
    optional:
      - string                  # Optional context files

  triggers:
    keywords:
      - string                  # Activation keywords
    file_patterns:
      - string                  # File patterns that activate agent

  outputs:
    - type: string              # Output type (document, analysis, code)
      format: string            # Output format (markdown, json, etc.)
```

### Optional Fields

```yaml
agent:
  dependencies:
    agents:
      - string                  # Other agents this depends on
    skills:
      - string                  # Skills this agent uses

  constraints:
    max_tokens: number          # Maximum output tokens
    temperature: number         # LLM temperature (0-1)

  examples:
    - input: string             # Example input
      output: string            # Expected output

  metadata:
    owner: string               # Team or person responsible
    created: date               # Creation date
    updated: date               # Last update date
```

### Example Agent Definition

```yaml
agent:
  id: ai-data-analyst
  name: AI Data Analyst
  description: Analyzes product metrics, creates dashboards, and generates insights
  version: "2.1.0"
  role: Data analysis and visualization

  capabilities:
    - Analyze product usage metrics
    - Create data visualizations
    - Generate cohort analyses
    - Build interactive dashboards
    - Identify trends and anomalies

  context:
    required:
      - context/data/insights/
      - context/data/churn-analysis/
    optional:
      - context/data/business/

  triggers:
    keywords:
      - metrics
      - analytics
      - churn
      - dashboard
      - funnel
    file_patterns:
      - "**/*.csv"
      - "**/dashboard*.html"

  outputs:
    - type: analysis
      format: markdown
    - type: visualization
      format: html
    - type: data
      format: csv

  dependencies:
    skills:
      - pipeline-metrics-analyzer

  metadata:
    owner: Data Team
    created: 2025-06-15
    updated: 2026-01-10
```

---

## Command Schema

### Required Fields

```yaml
command:
  name: string                  # Command name (without /)
  description: string           # Brief description
  version: string               # Semantic version

  parameters:
    - name: string              # Parameter name
      type: string              # Parameter type
      required: boolean         # Is required?
      description: string       # Parameter description
      default: any              # Default value (if optional)

  workflow:
    steps:
      - name: string            # Step name
        agent: string           # Agent to execute (optional)
        skill: string           # Skill to use (optional)
        action: string          # Action description

  outputs:
    - type: string              # Output type
      format: string            # Output format
```

### Example Command Definition

```yaml
command:
  name: discovery-orchestrator
  description: Orchestrates the full discovery process for new features
  version: "1.3.0"

  parameters:
    - name: feature
      type: string
      required: true
      description: Feature name or ID to run discovery for

    - name: depth
      type: enum
      required: false
      description: Discovery depth level
      default: standard
      options:
        - quick
        - standard
        - deep

    - name: include-competitive
      type: boolean
      required: false
      description: Include competitive analysis
      default: true

  workflow:
    steps:
      - name: Context Gathering
        agent: ai-pm
        action: Gather existing context and documentation

      - name: User Research
        agent: ai-user-researcher
        action: Analyze user feedback and interview data

      - name: Data Analysis
        agent: ai-data-analyst
        action: Analyze relevant metrics and trends

      - name: Competitive Analysis
        agent: competitive-benchmarking
        action: Research competitor approaches
        condition: include-competitive == true

      - name: Synthesis
        agent: product-manager
        action: Synthesize findings into discovery summary

  outputs:
    - type: document
      format: markdown
      name: DISCOVERY_SUMMARY.md
```

---

## Skill Schema

### Required Fields

```yaml
skill:
  id: string                    # Unique identifier (kebab-case)
  name: string                  # Human-readable name
  description: string           # Brief description
  version: string               # Semantic version

  inputs:
    - name: string              # Input name
      type: string              # Input type
      required: boolean         # Is required?
      description: string       # Input description

  outputs:
    - name: string              # Output name
      type: string              # Output type
      format: string            # Output format

  process:
    steps:
      - string                  # Processing steps
```

### Optional Fields

```yaml
skill:
  templates:
    - name: string              # Template name
      path: string              # Template file path

  validations:
    - name: string              # Validation name
      rule: string              # Validation rule
      message: string           # Error message

  examples:
    - input: object             # Example input
      output: object            # Expected output
```

### Example Skill Definition

```yaml
skill:
  id: prd-compliance-validator
  name: PRD Compliance Validator
  description: Validates PRD documents against NexusFlow standards
  version: "1.5.0"

  inputs:
    - name: prd_content
      type: string
      required: true
      description: The PRD content to validate

    - name: template
      type: enum
      required: false
      description: Template to validate against
      default: full
      options:
        - full
        - onepage
        - quickwin

  outputs:
    - name: validation_result
      type: object
      format: json
    - name: report
      type: document
      format: markdown

  validations:
    - name: has_problem_statement
      rule: "sections.problem != null"
      message: "PRD must include a problem statement"

    - name: has_success_metrics
      rule: "sections.metrics.length >= 3"
      message: "PRD must define at least 3 success metrics"

    - name: has_user_stories
      rule: "sections.user_stories.length >= 1"
      message: "PRD must include at least one user story"

    - name: okr_aligned
      rule: "okr_reference != null"
      message: "PRD must reference aligned OKRs"

  process:
    steps:
      - Parse PRD content into sections
      - Run each validation rule
      - Calculate compliance score
      - Generate detailed report
      - Provide improvement suggestions

  examples:
    - input:
        prd_content: "# Feature: Smart Onboarding..."
        template: full
      output:
        compliance_score: 85
        passed: 12
        failed: 2
        warnings: 3
```

---

## Context File Schema

### Business Context

```yaml
business_context:
  company:
    name: string
    description: string
    industry: string
    region: string
    stage: string

  product:
    name: string
    description: string
    target_market: string
    value_proposition: string

  metrics:
    current:
      - name: string
        value: number
        unit: string
    targets:
      - name: string
        value: number
        unit: string
        timeline: string

  teams:
    - name: string
      focus: string
      members: number
```

### PRD Structure

```yaml
prd:
  metadata:
    id: string
    title: string
    author: string
    created: date
    status: enum           # draft, review, approved, in-progress, shipped
    team: string
    quarter: string

  sections:
    problem:
      statement: string
      evidence: string[]
      impact: string

    solution:
      hypothesis: string
      approach: string
      scope: string

    user_stories:
      - persona: string
        action: string
        benefit: string

    requirements:
      functional:
        - string
      non_functional:
        - string

    metrics:
      primary:
        - name: string
          baseline: number
          target: number
      secondary:
        - name: string
          baseline: number
          target: number

    timeline:
      milestones:
        - name: string
          date: date
          deliverables: string[]

    risks:
      - risk: string
        probability: enum    # low, medium, high
        impact: enum         # low, medium, high
        mitigation: string
```

---

## Validation Rules

### Common Validations

| Field Type | Validation | Example |
|------------|------------|---------|
| id | kebab-case, unique | `ai-data-analyst` |
| version | semver | `1.2.3` |
| date | ISO 8601 | `2026-01-15` |
| enum | predefined values | `draft`, `review`, `approved` |
| percentage | 0-100 | `85` |
| currency | ISO code + value | `EUR 199.00` |

### File Naming

| Component | Pattern | Example |
|-----------|---------|---------|
| Agent | `[agent-id].md` | `ai-data-analyst.md` |
| Command | `[command-name].md` | `discovery-orchestrator.md` |
| Skill | `[skill-id]/SKILL.md` | `prd-compliance-validator/SKILL.md` |
| PRD | `[NN]_[Type].md` | `04_PRD.md` |
| Data | `[TOPIC]-[PERIOD].md` | `CHURN-ANALYSIS-Q1-2026.md` |

---

## Schema Version

- **Current Version**: 2.0.0
- **Last Updated**: January 2026
- **Maintainer**: Product Platform Team
