# Custom Slash Command Writer

## Command

```
/custom-slash-command-writer
```

## Version
1.1.0

## Description

The Custom Slash Command Writer helps create new custom commands for the NexusFlow product repository. It guides you through defining command behavior, parameters, and integration with existing agents and skills.

## When to Use

- Creating a new automated workflow
- Wrapping complex multi-step processes
- Standardizing team workflows
- Extending the command system

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `name` | string | Yes | - | Command name (without /) |
| `description` | string | Yes | - | What the command does |
| `template` | enum | No | standard | basic, standard, orchestrator |

## Usage Examples

```bash
# Create basic command
/custom-slash-command-writer name="generate-release-notes" description="Generate release notes from recent PRDs"

# Create orchestrator command
/custom-slash-command-writer name="quarterly-review" description="Run quarterly product review" template=orchestrator
```

## Command Templates

### Basic Template
Simple command with direct execution, no agent coordination.

```markdown
# [Command Name] Command

## Command

\`\`\`
/[command-name]
\`\`\`

## Version
1.0.0

## Description
[What this command does]

## Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|

## Usage Examples
\`\`\`bash
/[command-name] [example usage]
\`\`\`

## Workflow
1. [Step 1]
2. [Step 2]

## Output Format
[Expected output]

## Metadata
- **Owner**: [Team]
- **Created**: [Date]
```

### Standard Template
Command with agent integration and structured workflow.

```markdown
# [Command Name] Command

## Command

\`\`\`
/[command-name]
\`\`\`

## Version
1.0.0

## Description
[Detailed description]

## When to Use
[Use cases]

## Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|

## Usage Examples
\`\`\`bash
/[command-name] [examples]
\`\`\`

## Workflow

### Phase 1: [Name]
[Description]

### Phase 2: [Name]
[Description]

## Output Format
[Detailed output specification]

## Integration

### Agents Used
| Agent | Purpose |
|-------|---------|

### Skills Used
| Skill | Purpose |
|-------|---------|

## Error Handling
| Error | Handling |
|-------|----------|

## Metadata
- **Owner**: [Team]
- **Created**: [Date]
- **Updated**: [Date]
```

### Orchestrator Template
Complex command coordinating multiple agents with parallel/sequential execution.

```markdown
# [Command Name] Orchestrator Command

## Command

\`\`\`
/[command-name]
\`\`\`

## Version
1.0.0

## Description
[Detailed description of orchestration]

## When to Use
[Complex use cases]

## Parameters
| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|

## Orchestration Flow

\`\`\`
[ASCII diagram of agent coordination]
\`\`\`

## Phases

### Phase 1: [Name]
**Agent**: [agent-id]
**Input**: [What it receives]
**Output**: [What it produces]

### Phase 2: [Name]
**Agents**: [Parallel agents]
**Dependencies**: [What it needs from Phase 1]

### Phase 3: Synthesis
**Agent**: [Synthesizing agent]
**Input**: [All previous outputs]
**Output**: [Final deliverable]

## Output Format
[Comprehensive output specification]

## Integration

### Agents Used
| Agent | Phase | Mandatory |
|-------|-------|-----------|

### Skills Used
| Skill | Purpose |
|-------|---------|

### Dependencies
[External dependencies]

## Error Handling
| Scenario | Handling |
|----------|----------|

## Performance
| Metric | Target |
|--------|--------|

## Metadata
- **Owner**: [Team]
- **Created**: [Date]
- **Updated**: [Date]
```

## Creation Workflow

### Step 1: Define Purpose
- What problem does this command solve?
- Who will use it?
- How often will it be used?

### Step 2: Design Parameters
- What inputs are needed?
- Which are required vs optional?
- What are sensible defaults?

### Step 3: Design Workflow
- What steps are involved?
- Can steps run in parallel?
- What agents/skills are needed?

### Step 4: Define Output
- What should the command produce?
- What format is most useful?
- How will output be used?

### Step 5: Handle Errors
- What can go wrong?
- How should errors be handled?
- What fallbacks exist?

### Step 6: Document & Test
- Write comprehensive documentation
- Test with sample inputs
- Validate with intended users

## Validation Checklist

### Required Elements
- [ ] Command name (no spaces, lowercase, hyphens)
- [ ] Version number (semver)
- [ ] Description (clear, concise)
- [ ] Parameters table (complete)
- [ ] Usage examples (realistic)
- [ ] Workflow description
- [ ] Output format specification

### Quality Checks
- [ ] Name is intuitive
- [ ] Parameters have sensible defaults
- [ ] Error handling is comprehensive
- [ ] Documentation is complete
- [ ] Examples are copy-pasteable

## Best Practices

### Naming Conventions
- Use kebab-case: `generate-report`
- Be specific: `generate-prd-report` not `generate-report`
- Use verbs: `analyze-`, `generate-`, `validate-`

### Parameter Design
- Minimize required parameters
- Provide intelligent defaults
- Use enums for fixed choices
- Validate input ranges

### Documentation
- Lead with "when to use"
- Provide realistic examples
- Document all edge cases
- Include troubleshooting

### Error Handling
- Never fail silently
- Provide actionable error messages
- Include recovery suggestions
- Log for debugging

## File Location

Commands are stored in:
```
.claude/commands/[command-name].md
```

## Registration

After creating a command, update:
1. `.claude/COMPONENT_INDEX.md` - Add to commands list
2. `.claude/SELECTION_RULES.md` - Add trigger keywords

## Example: Creating a Command

### Input
```bash
/custom-slash-command-writer name="weekly-standup-prep" description="Prepare weekly standup summary from recent activity"
```

### Generated Command

```markdown
# Weekly Standup Prep Command

## Command

\`\`\`
/weekly-standup-prep
\`\`\`

## Version
1.0.0

## Description

Generates a weekly standup summary by analyzing recent PRD updates, data changes, and team activity to prepare talking points for the weekly product standup.

## When to Use

- Before weekly product standup meetings
- When preparing status updates for stakeholders
- To get a quick summary of the week's progress

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| team | string | No | all | Filter by team |
| days | number | No | 7 | Days to look back |
| format | enum | No | summary | summary, detailed, bullets |

## Usage Examples

\`\`\`bash
# Default summary for all teams
/weekly-standup-prep

# Specific team, last 5 days
/weekly-standup-prep team=activation days=5

# Detailed format
/weekly-standup-prep format=detailed
\`\`\`

## Workflow

### Phase 1: Activity Collection
Scan recent changes in:
- PRDs (new, updated, completed)
- Discovery documents
- Data reports
- Strategy updates

### Phase 2: Synthesis
Summarize into categories:
- Completed items
- In progress items
- Blockers/risks
- Upcoming priorities

## Output Format

\`\`\`markdown
# Weekly Standup: [Date Range]

## Completed
- [Item 1]
- [Item 2]

## In Progress
- [Item 1]: [Status]
- [Item 2]: [Status]

## Blockers
- [Blocker if any]

## This Week's Focus
- [Priority 1]
- [Priority 2]
\`\`\`

## Metadata
- **Owner**: Product Team
- **Created**: 2026-01-15
```

## Metadata

- **Owner**: Product Platform Team
- **Created**: 2025-10-01
- **Updated**: 2026-01-10
