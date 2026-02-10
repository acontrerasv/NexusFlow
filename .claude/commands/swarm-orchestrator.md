# Swarm Orchestrator Command

## Command

```
/swarm-orchestrator
```

## Version
1.2.0

## Description

The Swarm Orchestrator coordinates multiple agents working in parallel on complex, multi-faceted tasks. It manages agent collaboration, handles dependencies, and synthesizes outputs from multiple specialists.

## When to Use

- Complex tasks requiring multiple perspectives
- Parallel work streams that need coordination
- Large initiatives spanning multiple domains
- When speed is critical and parallel execution helps

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `task` | string | Yes | - | Description of the task |
| `agents` | string[] | No | auto | Agents to include |
| `mode` | enum | No | parallel | parallel, sequential, hybrid |
| `timeout` | number | No | 30 | Max minutes per agent |
| `synthesis` | boolean | No | true | Synthesize outputs |

## Usage Examples

```bash
# Auto-select agents for task
/swarm-orchestrator task="Design new enterprise onboarding flow"

# Specify agents
/swarm-orchestrator task="Technical specification for CRM sync v2" agents=["ai-architect-engineer", "ai-frontend-engineer", "product-manager"]

# Sequential mode for dependent tasks
/swarm-orchestrator task="Full PRD with technical review" mode=sequential
```

## Orchestration Modes

### Parallel Mode
All agents work simultaneously, outputs merged at end.

```
┌─────────────────────────────────────────────────────────┐
│                     ORCHESTRATOR                         │
└─────────────────────┬───────────────────────────────────┘
                      │ Task Distribution
        ┌─────────────┼─────────────┐
        ▼             ▼             ▼
   ┌─────────┐   ┌─────────┐   ┌─────────┐
   │ Agent 1 │   │ Agent 2 │   │ Agent 3 │
   └────┬────┘   └────┬────┘   └────┬────┘
        │             │             │
        └─────────────┼─────────────┘
                      ▼
              ┌───────────────┐
              │   SYNTHESIS   │
              └───────────────┘
```

### Sequential Mode
Agents work in order, each building on previous output.

```
┌─────────────┐   ┌─────────────┐   ┌─────────────┐
│   Agent 1   │──▶│   Agent 2   │──▶│   Agent 3   │
└─────────────┘   └─────────────┘   └─────────────┘
       │                 │                 │
       ▼                 ▼                 ▼
   [Output 1]   [Output 1 + 2]   [Final Output]
```

### Hybrid Mode
Critical path sequential, supporting tasks parallel.

```
                    ┌─────────────┐
          ┌────────▶│   Agent 2   │────────┐
          │         └─────────────┘        │
┌─────────┴───┐                       ┌────▼────────┐
│   Agent 1   │                       │   Agent 4   │
└─────────┬───┘                       └─────────────┘
          │         ┌─────────────┐        │
          └────────▶│   Agent 3   │────────┘
                    └─────────────┘
```

## Agent Selection Logic

### Auto-Selection Rules

| Task Keywords | Selected Agents |
|---------------|-----------------|
| "PRD", "feature", "requirements" | product-manager, ai-architect-engineer |
| "design", "UX", "flow" | ai-product-designer, ai-frontend-engineer |
| "technical", "architecture" | ai-architect-engineer, ai-data-ml-engineer |
| "research", "user", "interview" | ai-user-researcher, ai-data-analyst |
| "metrics", "data", "analysis" | ai-data-analyst, product-usage-analyst |
| "launch", "marketing" | ai-product-marketing, product-manager |

### Agent Compatibility Matrix

| Agent | Works Well With | Avoid Pairing |
|-------|-----------------|---------------|
| product-manager | ai-architect-engineer, ai-product-designer | - |
| ai-architect-engineer | ai-frontend-engineer, ai-data-ml-engineer | - |
| ai-data-analyst | product-usage-analyst, ai-pm | - |
| ai-user-researcher | ai-product-designer, product-manager | - |

## Workflow

### Step 1: Task Analysis
1. Parse task description
2. Identify required capabilities
3. Select appropriate agents
4. Determine execution mode

### Step 2: Work Distribution
1. Break task into agent-specific subtasks
2. Identify dependencies
3. Create execution plan
4. Set timeouts

### Step 3: Execution
1. Launch agents (parallel or sequential)
2. Monitor progress
3. Handle timeouts/errors
4. Collect outputs

### Step 4: Synthesis
1. Gather all agent outputs
2. Identify conflicts/overlaps
3. Merge into coherent result
4. Generate final output

## Output Format

```markdown
# Swarm Output: [Task]

## Execution Summary
- **Task**: [Description]
- **Mode**: [parallel/sequential/hybrid]
- **Agents**: [List of agents used]
- **Duration**: [Total time]
- **Status**: [Success/Partial/Failed]

## Agent Contributions

### [Agent 1 Name]
**Focus**: [What they worked on]
**Key Output**:
[Summary of their contribution]

### [Agent 2 Name]
**Focus**: [What they worked on]
**Key Output**:
[Summary of their contribution]

## Synthesized Result

### Summary
[Merged, coherent summary of all contributions]

### Key Findings
1. [Finding 1]
2. [Finding 2]
3. [Finding 3]

### Recommendations
1. [Recommendation 1]
2. [Recommendation 2]

### Conflicts/Considerations
[Any disagreements between agents or tradeoffs to consider]

## Detailed Outputs

### [Agent 1] Full Output
[Complete output from agent 1]

### [Agent 2] Full Output
[Complete output from agent 2]

## Next Steps
1. [Action item]
2. [Action item]
```

## Error Handling

| Scenario | Handling |
|----------|----------|
| Agent timeout | Continue with available outputs, note gap |
| Agent failure | Retry once, then proceed without |
| No agents available | Error with suggestions |
| Conflicting outputs | Flag in synthesis, present both views |

## Common Swarm Patterns

### PRD Development Swarm
```yaml
agents:
  - product-manager      # PRD writing
  - ai-architect-engineer # Technical feasibility
  - ai-product-designer   # UX considerations
mode: hybrid
flow:
  1. product-manager creates draft
  2. parallel: architect + designer review
  3. product-manager incorporates feedback
```

### Feature Analysis Swarm
```yaml
agents:
  - ai-data-analyst      # Quantitative analysis
  - ai-user-researcher   # Qualitative insights
  - competitive-benchmarking # Market context
mode: parallel
synthesis: ai-pm
```

### Technical Specification Swarm
```yaml
agents:
  - ai-architect-engineer # System design
  - ai-frontend-engineer  # Frontend specs
  - ai-data-ml-engineer   # AI/ML components
  - qa-expert            # Test strategy
mode: sequential
```

## Performance

| Mode | Typical Duration | Best For |
|------|-----------------|----------|
| Parallel | 15-30 min | Independent analysis |
| Sequential | 30-60 min | Dependent deliverables |
| Hybrid | 20-45 min | Mixed dependencies |

## Limitations

- Maximum 5 agents per swarm
- 30 minute timeout per agent (configurable)
- Sequential mode limited to 4 steps
- Cannot resolve all conflicts automatically

## Metadata

- **Owner**: Product Platform Team
- **Created**: 2025-09-01
- **Updated**: 2026-01-10
