# Introspection Lifecycle

An introspection's item in `.praxis/tracking/introspections/` holds its scope marker, the runs it read, its blind spots, and its forecasts. It is written by the introspection itself and scored by the introspections after it, so introspection is held to the outcomes that follow it.

## Stages

- Recorded
- Scored

## Stage Flow

State-machine grammar for this lifecycle:

```
New -> Recorded
Recorded -> Scored
Scored -> Cleared
```

## Stage 1: Recorded

The item is written and some forecast is not yet final. A later introspection may write partial scores (Too early) and the item stays Recorded.

**Entry Paths:**
- `praxis-create-introspection`

**Exit Paths:**
Scored:
- `praxis-refine-introspection` (every forecast is Hit, Miss, or Unscorable)

## Stage 2: Scored

Every forecast has a final score. The item stays as the record of how well that introspection saw ahead.

**Entry Paths:**
- `praxis-refine-introspection`

**Exit Paths:**
Cleared:
- `praxis-refine-introspection` (when the owner asks; git keeps the item)
