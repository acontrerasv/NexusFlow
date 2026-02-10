# Component State Machines

> State machine definitions for key NexusFlow entities.

## Overview

This document defines the state machines for major entities in NexusFlow. Understanding these states and transitions is essential for PRD writing and feature development.

---

## Workflow State Machine

### States

| State | Description | Entry Condition |
|-------|-------------|-----------------|
| `draft` | Being created/edited | New workflow created |
| `active` | Running, can be triggered | User activates |
| `paused` | Temporarily stopped | User pauses |
| `archived` | Soft deleted | User archives |

### Transitions

```
                    ┌──────────────────┐
                    │      draft       │
                    └────────┬─────────┘
                             │ activate
                             ▼
              ┌──────────────────────────────┐
   ┌──────────│           active             │◀──────────┐
   │          └──────────────────────────────┘           │
   │ pause                 │                    resume   │
   ▼                       │ archive                     │
┌──────────┐               │                    ┌────────┴───┐
│  paused  │───────────────┼───────────────────▶│  archived  │
└──────────┘    archive    │                    └────────────┘
                           ▼
                    ┌──────────────────┐
                    │    archived      │
                    └──────────────────┘
```

### Transition Rules

| From | To | Trigger | Conditions |
|------|-----|---------|------------|
| draft | active | User activates | Valid config |
| draft | archived | User archives | - |
| active | paused | User pauses | - |
| active | draft | User edits | - |
| active | archived | User archives | - |
| paused | active | User resumes | - |
| paused | draft | User edits | - |
| paused | archived | User archives | - |
| archived | draft | User restores | - |

---

## Workflow Execution State Machine

### States

| State | Description | Entry Condition |
|-------|-------------|-----------------|
| `pending` | Queued for execution | Trigger fired |
| `running` | Currently executing | Worker picks up |
| `completed` | Successfully finished | All steps done |
| `failed` | Execution failed | Error occurred |
| `cancelled` | User cancelled | User action |
| `timeout` | Exceeded time limit | Time limit hit |

### Transitions

```
┌──────────┐
│ pending  │
└────┬─────┘
     │ start
     ▼
┌──────────┐      ┌───────────┐
│ running  │─────▶│ completed │
└────┬─────┘      └───────────┘
     │
     ├─────────────▶ failed
     │    error
     │
     ├─────────────▶ cancelled
     │    cancel
     │
     └─────────────▶ timeout
          timeout
```

### Transition Rules

| From | To | Trigger | Conditions |
|------|-----|---------|------------|
| pending | running | Worker starts | Worker available |
| pending | cancelled | User cancels | - |
| running | completed | All steps done | No errors |
| running | failed | Error occurs | Error not recoverable |
| running | cancelled | User cancels | - |
| running | timeout | Time exceeded | timeout_minutes exceeded |
| failed | pending | Retry | retry_count < max_retries |

### Execution Data

```typescript
interface WorkflowExecution {
  id: string;
  workflow_id: string;
  status: 'pending' | 'running' | 'completed' | 'failed' | 'cancelled' | 'timeout';
  started_at: Date | null;
  completed_at: Date | null;
  error: string | null;
  retry_count: number;
  steps: StepExecution[];
}
```

---

## User Account State Machine

### States

| State | Description | Entry Condition |
|-------|-------------|-----------------|
| `pending` | Awaiting verification | Account created |
| `active` | Normal operation | Email verified |
| `suspended` | Temporarily disabled | Admin action |
| `deactivated` | User-initiated disable | User request |
| `deleted` | Permanently removed | Deletion request |

### Transitions

```
┌──────────┐
│ pending  │
└────┬─────┘
     │ verify_email
     ▼
┌──────────┐      ┌───────────┐
│  active  │◀────▶│ suspended │
└────┬─────┘      └───────────┘
     │ deactivate      │
     ▼                 │ delete
┌────────────┐         │
│deactivated │─────────┤
└────────────┘         │
     │                 │
     └─────────────────┼─────────▶ deleted
          delete       │
```

### Transition Rules

| From | To | Trigger | Conditions |
|------|-----|---------|------------|
| pending | active | Email verified | Valid token |
| pending | deleted | Timeout | 7 days unverified |
| active | suspended | Admin suspends | Admin action |
| active | deactivated | User deactivates | User request |
| active | deleted | User requests deletion | After 30 day wait |
| suspended | active | Admin reactivates | Admin action |
| suspended | deleted | Admin deletes | Admin action |
| deactivated | active | User reactivates | Within 90 days |
| deactivated | deleted | Grace period ends | After 90 days |

---

## Subscription State Machine

### States

| State | Description | Entry Condition |
|-------|-------------|-----------------|
| `trialing` | Free trial period | New signup |
| `active` | Paying customer | Trial converts or direct subscribe |
| `past_due` | Payment failed | Payment failure |
| `cancelled` | Subscription ended | User cancels |
| `expired` | Trial ended without conversion | Trial timeout |

### Transitions

```
┌───────────┐
│  trialing │
└─────┬─────┘
      │ convert
      ├─────────────────────────────┐
      │                             │
      ▼                             ▼
┌───────────┐                 ┌───────────┐
│   active  │◀───────────────▶│ past_due  │
└─────┬─────┘    payment      └─────┬─────┘
      │ cancel   cycle              │
      │                             │ 3 failures
      ▼                             ▼
┌───────────┐                 ┌───────────┐
│ cancelled │                 │ cancelled │
└───────────┘                 └───────────┘

┌───────────┐
│  trialing │
└─────┬─────┘
      │ trial_ends
      ▼
┌───────────┐
│  expired  │
└───────────┘
```

### Transition Rules

| From | To | Trigger | Conditions |
|------|-----|---------|------------|
| trialing | active | User subscribes | Valid payment |
| trialing | expired | Trial ends | No conversion |
| active | past_due | Payment fails | Payment declined |
| active | cancelled | User cancels | - |
| past_due | active | Payment succeeds | Retry succeeds |
| past_due | cancelled | 3 failures | Max retries exceeded |
| expired | active | User subscribes | Valid payment |
| cancelled | active | User resubscribes | Valid payment |

---

## Integration Connection State Machine

### States

| State | Description | Entry Condition |
|-------|-------------|-----------------|
| `disconnected` | Not connected | Initial or disconnected |
| `connecting` | OAuth in progress | User initiates |
| `connected` | Successfully linked | OAuth complete |
| `error` | Connection issue | Sync/auth error |
| `refreshing` | Refreshing token | Token expired |

### Transitions

```
┌──────────────┐
│ disconnected │
└──────┬───────┘
       │ initiate
       ▼
┌──────────────┐      ┌───────────┐
│  connecting  │─────▶│ connected │
└──────┬───────┘      └─────┬─────┘
       │ fail               │
       │                    │ error
       ▼                    ▼
┌──────────────┐      ┌───────────┐
│ disconnected │◀─────│   error   │
└──────────────┘      └───────────┘
                            │
                            │ recover
                            ▼
                      ┌───────────┐
                      │ connected │
                      └───────────┘
```

---

## PRD State Machine

### States

| State | Description | Entry Condition |
|-------|-------------|-----------------|
| `draft` | Being written | PRD created |
| `review` | Under review | Submitted for review |
| `approved` | Ready for development | Reviewers approve |
| `in_progress` | Being built | Development started |
| `shipped` | Released | Feature launched |
| `deprecated` | No longer relevant | Sunset or pivoted |

### Transitions

```
┌────────┐
│ draft  │
└───┬────┘
    │ submit
    ▼
┌────────┐      ┌──────────┐
│ review │─────▶│ approved │
└───┬────┘      └────┬─────┘
    │                │ start_dev
    │ reject         ▼
    │           ┌────────────┐
    │           │in_progress │
    │           └────┬───────┘
    ▼                │ ship
┌────────┐           ▼
│ draft  │      ┌──────────┐
└────────┘      │ shipped  │
                └────┬─────┘
                     │ deprecate
                     ▼
                ┌────────────┐
                │ deprecated │
                └────────────┘
```

---

## State Machine Best Practices

### For PRD Writers

1. **Document all states** - List every state the feature can be in
2. **Define transitions** - Specify what triggers state changes
3. **Handle edge cases** - What happens in error states?
4. **Consider rollback** - Can users go back?

### For Engineers

1. **Validate transitions** - Don't allow invalid state changes
2. **Log state changes** - Audit trail for debugging
3. **Handle race conditions** - Use optimistic locking
4. **Expose state in API** - Clients need to know current state

### Template

```markdown
## [Entity] State Machine

### States
| State | Description | Entry Condition |
|-------|-------------|-----------------|

### Transitions
[State diagram]

### Transition Rules
| From | To | Trigger | Conditions |
|------|-----|---------|------------|

### Side Effects
| Transition | Side Effects |
|------------|--------------|
```

---

*Last Updated: January 2026*
