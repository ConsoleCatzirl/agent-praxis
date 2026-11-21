# Outcome Lifecycle

This document defines the lifecycle stages for plans tracked in `.praxis/state/outcomes.md`.
An Outcome is the list of effects and results from performing a Plan.

## Stages

- Actualized
- Analyzed

## Stage Flow

```
New -> [ Actualized | Bypassed ]
Actualized -> Analyzed
[ Analyzed | Bypassed ] -> Cleared
```

## Stage 1: Actualized

The Outcome has been Actualized and documented in `.praxis/state/outcomes.md`

**Entry Paths:**
- `praxis-flow-act`

**Exit Paths:**
Analyzed:
- `praxis-analyze`

## Stage 2: Analyzed

The outcome has been analyzed.

**Entry Paths:**
- `praxis-analyze`

**Exit Paths:**
Cleared:
- `praxis-clear`

## Stage 3: Bypassed

A Plan for all Trivial complexity Tasks, bypassing planning prediction, and disernment

**Entry Paths:**
- `praxis-decompose`

**Exit Paths:**
Cleared:
- `praxis-clear`
