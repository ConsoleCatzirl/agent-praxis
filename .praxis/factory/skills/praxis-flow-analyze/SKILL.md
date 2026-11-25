---
name: praxis-flow-analyze
description: Analyze the outcome of performing a plan
---

# Skill: Praxis Analyze

Compare the actualized outcomes with predicted outcomes.

## Origin
Praxis Template

## Purpose
Compare predicted results with actualized results

## When to Use
After performing the current Plans

## How it Works
Compare the list of expected and actualized outcomes to determine surprises and result classification.

## Requirements

Either an Actualized Prediction and its Actualized Outcome, or a Rejected Prediction.

## Inputs

Either an Actualized Prediction and its Actualized Outcome, or a Rejected Prediction.

## Procedure

As Outcomes are created in `.praxis/state/outcomes/`:
  1. Review the Outcome's Plan, and that Plan's Prediction.
  2. Review any revisions of the Outcome's Plan and their Predictions.
  3. Create a new Analysis in `.praxis/state/analyses/` from the template `.praxis/templates/analysis-template.md`.
  4. Mark the relevant Predictions Analyzed.
  5. Mark the Outcome Analyzed.
  4. Summarize any surprises.

## Output

A Created Analysis.

## Success Criteria

Analysis is successfully written to state.

## Domain Alignment

## Related Skills

- praxis-\*

## Troubleshooting
