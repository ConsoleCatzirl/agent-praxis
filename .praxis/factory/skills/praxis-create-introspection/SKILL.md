---
name: praxis-create-introspection
description: Write an introspection's item in `.praxis/tracking/introspections/`, with its scope marker, runs read, blind spots, and falsifiable forecasts for later introspections to score.
confidence: Low
---

# Skill: Praxis Create Introspection

## Origin
Written for this template as a mechanism of the factory, with no recorded use.

## Purpose
Hold an introspection to the outcomes that follow it: record what it forecast, so that later introspections can score the forecasts.

## When to Use
At the forecast step of `praxis-flow-introspect`, after its findings are written.

## How it Works
The skill chooses three to five forecasts tied to findings, writes the item from the introspection template in the Recorded stage, lists it, and commits.

## Requirements
- The introspection's findings, its run count and its blind spots.
- `.praxis/templates/introspection-template.md` and `.praxis/lifecycles/introspection-lifecycle.md` have been read.

## Inputs
The Plan's name, the number of runs read and their `Clear state` commits, the blind spots by kind, and the findings.

## Procedure
1. Read `.praxis/templates/introspection-template.md`, `.praxis/lifecycles/introspection-lifecycle.md` and `.praxis/tracking/introspections.md`.
2. Choose three to five forecasts about the runs after this one, each tied to a finding: what a fix should move, or what will go on if nothing changes. Write each as `<mean|sum|min|max> <metric> <op> <number> over <N> runs -- <the finding>`, with the threshold set from the metric's values in recent runs. Prefer a forecast that could miss over one that cannot.
3. Create the item `.praxis/tracking/introspections/${date}-${name}.md` from the template: Status `Recorded`, both timestamps from `date -Iseconds`, the marker (the repository's HEAD when the item is written), the runs read, the blind spots, and every forecast.
4. Add the item to `.praxis/tracking/introspections.md`, oldest first.
5. Commit the item and the list as one logical change.

## Output
A Recorded item in `.praxis/tracking/introspections/` and its entry in `.praxis/tracking/introspections.md`.

## Success Criteria
- Every forecast names a metric, an operator, a number and a number of runs, and could be scored Hit or Miss.
- The item is in the Recorded stage and listed.

## Domain Alignment

Aligned
- Rule: Praxis Records MUST Conform to Their Templates and Lifecycles

Unaligned
- none known

## Related Skills

- praxis-refine-introspection
- praxis-flow-introspect

## Troubleshooting

### Issue: The forecasts cannot miss

Identifying:
Every threshold is already met by the recent values.

Solution:
Reset the thresholds, and record in Notes that the history guaranteed the first set.
