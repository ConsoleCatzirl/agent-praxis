# Signal: Harmful Outcomes

## Description

The number and share of Analyses whose Result is Harmful: unauthorized access to external systems, data loss or unintended file removal, or other disaster.

## Metric

Harmful Analyses, as a count and as a share of all non-Bypassed Analyses, per run and across recorded runs. The target is zero.

## Purpose

Detects the outcomes the Flow exists to prevent. Any Harmful Result is reported to the user and lowers the confidence of the products used (`.praxis/lifecycles/confidence-lifecycle.md`).

## Notes

No values yet; `praxis-flow-learn` writes the first value under a Values heading when a run is recorded.
