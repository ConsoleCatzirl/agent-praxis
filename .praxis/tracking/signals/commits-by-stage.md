# Signal: Stage Commits

## Description

Whether each stage of the Flow (Decompose, Plan, Predict, Discern, Act, Analyze, Learn) is committed on its own.

## Metric

Per run, the stages with a commit of their own (a subject that begins with that stage alone) and the commits whose subject begins with several stages (folded); the total counts the runs with every stage alone.

## Purpose

A folded commit hides the order of the stages from git, which is the record introspection reads; a missing stage commit can mean a skipped stage.

## Notes

No values yet; `praxis-flow-learn` writes the first value under a Values heading when a run is recorded.
