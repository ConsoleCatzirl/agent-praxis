---
name: praxis-refine-introspection
description: Score the forecasts of earlier introspections, move an item to Scored when every forecast is final, and correct or clear items.
confidence: Low
---

# Skill: Praxis Refine Introspection

## Origin
Praxis Template

## Purpose
Close the loop on introspection: say which forecasts held, so that introspection is judged by what followed it.

## When to Use
When an introspection runs and earlier items are Recorded, or an item must be corrected or cleared.

## How it Works
The skill reads each Recorded item's forecasts against the metrics of the runs since its marker, writes each score, and moves an item to Scored when none is still too early.

## Requirements
At least one item in `.praxis/tracking/introspections/`.

## Inputs
The name of the scoring introspection (its Plan), or the item to correct and the reason.

## Procedure
1. Read every Recorded item in `.praxis/tracking/introspections/` and the metrics of the runs since its marker.
2. Score each forecast Hit, Miss, Unscorable or Too early, with the value found, in a Scores section of the item naming the scoring Plan. An item with a Too early forecast stays Recorded; when every forecast is Hit, Miss or Unscorable, set its Status to Scored.
3. For each Miss, write in Notes what the forecast assumed and what happened instead, and whether the finding behind it was wrong or its fix did not work; say so when a Hit was on a target the history already guaranteed. Update the item's modified timestamp from `date -Iseconds`.
4. To correct an item, edit only the field that is wrong, say what and why in Notes, and never change a forecast after it has been scored. To clear a Scored item, only when the owner asks, remove it with `git rm` and its line from the list; git keeps it.
5. Commit the items and `.praxis/tracking/introspections.md` as one logical change, and give the scores to the introspection's Outcome.

## Output
Scores written into the items, items moved to Scored when final, and the scores for the introspection's Outcome.

## Success Criteria
- Every scored forecast has its value and the scoring Plan named.
- An item is Scored only when no forecast is Too early.

## Domain Alignment

Aligned
- Rule: Praxis Records MUST Conform to Their Templates and Lifecycles

Unaligned
- none known

## Related Skills

- praxis-create-introspection
- praxis-flow-introspect

## Troubleshooting

### Issue: A forecast cannot be scored

Identifying:
The metric it names is not recorded in the runs.

Solution:
Score it Unscorable and say which metric is missing.
