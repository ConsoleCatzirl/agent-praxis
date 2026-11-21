# Prediction Lifecycle

This document defines the lifecycle stages for plans tracked in `.praxis/state/predictions.md`.
Predictions are anticipations of task outcomes made during the Anticipate phase.

## Stages

- Created
- Approved
- Rejected
- Actualized
- Analyzed
- Bypassed

## Stage Flow

State-machine grammar for this lifecycle:

```
New -> [ Created | Bypassed ]
Created -> [ Rejected | Approved ]
Approved -> Actualized
[ Rejected | Actualized ] -> Analyzed
[ Analyzed | Bypassed ] -> Cleared
```

## Stage 1: Created

Anticipated outcomes are documented in memory/predictions.md

**Entry Paths:**
- `praxis-predict`

**Exit Paths:**
Approved:
- `praxis-discern`
Rejected:
- `praxis-discern`

## Stage 2: Rejected

Anticipated Outcomes are detrimental or harmful. No Actualized Outcomes.
The Plan must not be performed.

**Entry Paths:**
- `praxis-discern`

**Exit Paths:**
Analyzed:
- `praxis-analyze`

## Stage 3: Approved

This Prediction's Plan is approved and ready to be performed.

**Entry Paths:**
- `praxis-discern`

**Exit Paths:**
Actualized:
- `praxis-flow-act`

## Stage 4: Actualized

Actualized outcomes are documented in memory/predictions.md

**Entry Paths:**
- `praxis-flow-act`

**Exit Paths:**
Analyzed:
- `praxis-analyzed`

## Stage 5: Analyzed

Anticipated and Actualized outcomes (or rejection reason) have been compared and learnings have been documented.

**Entry Paths:**
- `praxis-analyze`

**Exit Paths:**
Cleared:
- `praxis-clear`

## Stage 6: Bypassed

A Plan for all Trivial complexity Tasks, bypassing planning prediction, and disernment

**Entry Paths:**
- `praxis-decompose`

**Exit Paths:**
Cleared:
- `praxis-clear`
