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
- `praxis-analyze`

**Exit Paths:**
Processed:
- `praxis-learn`

## Stage 2: Processed

Analysis updates have been applied.

**Entry Paths:**
- `praxis-learn`

**Exit Paths:**
Cleared:
- `praxis-clear`

## Stage 3: Bypassed

A Plan for all Trivial complexity Tasks, bypassing planning prediction, and disernment

**Entry Paths:**
- `praxis-decompose`

**Exit Paths:**
Processed:
- `praxis-learn`
