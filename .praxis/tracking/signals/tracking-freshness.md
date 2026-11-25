# Signal: Tracking Freshness

## Description

Whether a run updates the confidence tables it should: a run that uses factory products and changes no row of `tracking/confidence/*.csv` skipped Learn's tracking step.

## Metric

Per run, between the previous `Clear state` commit and the run's own: the rows of `tracking/confidence/*.csv` added or changed, and the lines added to `tracking/signals/*.md`; the totals count the runs with none of each.

## Purpose

Confidence moves only on recorded use; if use is not recorded, no level can ever move.

## Notes

No values yet; `praxis-flow-learn` writes the first value under a Values heading when a run is recorded.
