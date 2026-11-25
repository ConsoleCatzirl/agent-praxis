# Analysis Lifecycle

Analyses are created, processed, and then cleared.

## Stages

- Created
- Processed
- Bypassed

## Stage Flow

State-machine grammar for this lifecycle:

```
New -> [ Created | Bypassed ]
[ Created | Bypassed ] -> Processed
Processed -> Cleared
```

## Stage 1: Created

An analysis has been recorded.

**Entry Paths:**
- `praxis-flow-analyze`

**Exit Paths:**
Processed:
- `praxis-flow-learn`

## Stage 2: Processed

Analysis updates have been applied.

**Entry Paths:**
- `praxis-flow-learn`

**Exit Paths:**
Cleared:
- `praxis-flow-clear-state`

## Stage 3: Bypassed

A Plan for all Trivial complexity Tasks, bypassing planning prediction, and disernment

**Entry Paths:**
- `praxis-flow-decompose`

**Exit Paths:**
Processed:
- `praxis-flow-learn`
