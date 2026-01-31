---
description: Regenerate CLAUDE.md preserving progressive disclosure architecture (never use /init)
allowed-tools: Read, Write, Edit, Glob, Bash(ls:*), Bash(wc:*), Bash(tree:*)
---

## Current State

Repository structure:
!`tree -L 2 -d context/ .claude/ 2>/dev/null || ls -la context/ .claude/`

Current CLAUDE.md line count:
!`wc -l CLAUDE.md`

Available commands:
!`ls -1 .claude/commands/`

Available agents:
!`ls -1 .claude/agents/`

Available skills:
!`ls -1 .claude/skills/`

## Reference Files

Current CLAUDE.md structure: @CLAUDE.md
Reference docs index: @context/docs/

## Task

Regenerate CLAUDE.md while STRICTLY preserving the progressive disclosure architecture:

1. **Scan** for new commands, agents, skills, and directory changes
2. **Update** only the tables that need changes (Key Commands, Quick Agent Selection, Quick Skill Selection)
3. **Preserve** the WHY-WHAT-HOW structure exactly
4. **Maintain** all references to `context/docs/` files
5. **Validate** final line count is <150 lines

## Constraints

- NEVER add detailed content inline (keep in context/docs/)
- NEVER exceed 150 lines
- NEVER remove progressive disclosure references
- ALWAYS keep the `/init` warning in Key Commands section

## Output

Show a summary of changes made and validation results.
