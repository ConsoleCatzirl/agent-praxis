# Plan Lifecycle

This document defines the lifecycle stages for plans tracked in `.praxis/state/plans.md`.
A Plan is a list of Tasks to perform during Act

## Stages

- Proposed
- Approved
- Rejected
- Completed
- Bypassed

## Stage Flow

```
New -> [ Proposed | Bypassed ]
Proposed -> [ Approved | Rejected ]
Approved -> Completed
[ Rejected | Completed | Bypassed ] -> Cleared
```

## Stage 1: Proposed

A list of Plans are written that complete all Task criteria.

**Entry Paths:**
- `praxis-plan`

**Exit Paths:**
Approved:
- `praxis-discern`
Rejected:
- `praxis-discern`
- `praxis-prediction`

## Stage 2: Approved

The Plan is recorded and awaiting execution.

**Entry Paths:**
- `praxis-discern`

**Exit Paths:**
Completed:
- `praxis-flow-act`

## Stage 3: Completed

All Plans have finished execution. Document Outcomes and any artifacts produced.

**Entry Paths:**
- `praxis-flow-act`

**Exit Paths:**
Cleared:
- `praxis-clear`

## Stage 4: Rejected

Plan will not be performed.

**Entry Paths:**
- `praxis-prediction`
- `praxis-discern`

**Exit Paths:**
Cleared:
- `praxis-clear`

## Stage 5: Bypassed

A Plan for all Trivial complexity Tasks, bypassing planning prediction, and disernment

**Entry Paths:**
- `praxis-decompose`

**Exit Paths:**
Completed:
- `praxis-flow-act`
