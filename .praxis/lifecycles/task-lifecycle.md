# Task Lifecycle

Tasks are created during the Decompose phase with the purpose and criteria for the Plans created during the Plan phase of the Praxis Flow.

## Stages

- Identified
- Approved
- Rejected
- Completed

## Stage Flow

```
New -> Identified
Identified -> [ Approved | Rejected ]
Approved -> [ Completed | Rejected ]
[ Completed | Rejected ] -> Cleared
```

## Stage 0: Identified

The Tasks for the Plan Actions are documented.

**Entry Paths:**
- `praxis-create-task`

**Exit Paths:**
Approved:
- `praxis-flow-plan`
Rejected:
- `praxis-flow-plan`
- `praxis-flow-predict`

## Stage 1: Approved

The task is recorded and awaiting execution. Dependencies must be satisfied before moving to In Progress.

**Entry Paths:**
- `praxis-flow-plan`
- `praxis-flow-discern`

**Exit Paths:**
Completed:
- `praxis-flow-act`
Rejected:
- `praxis-flow-discern`

## Stage 2: Completed

All sub-tasks are finished. Document outcomes and any artifacts produced.

**Entry Paths:**
- `praxis-flow-act`

**Exit Paths:**
- `praxis-flow-clear-state`

## Stage 3: Rejected

Tasks will not be performed.

**Entry Paths:**
- `praxis-flow-plan`
- `praxis-flow-predict`
- `praxis-flow-discern`

**Exit Paths:**
- `praxis-flow-clear-state`
