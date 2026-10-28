---
name: praxis-discern
description: Determine whether or not act on a plan
---

# Skill: Praxis Discern

Review a Plan's Prediction and determine whether to act, alter the plan, or abort.

## Origin
Initial Implementation

## Purpose
Review Plans and their Predictions for approval or rejection.

## When to Use
After creating a Prediction, before performing its Plan

## How it Works

## Requirements

Created Prediction

## Inputs

Created Predicton

## Procedure

For each Plan with a Prediction, review the anticipated outcomes in the Prediction.
If any anticipated outcomes would be harmful, mark the Plan and its Prediction Rejected and continue to `praxis-analyze`.
If the anticipated outcomes don't fulfill all of the Plan's Tasks, mark the Plan and its Prediction Rejected and return to `praxis-plan` to revise the Plan with a new Prediction.
If there are no harmful anticipated outcomes and all respective Tasks would be completed, mark the Plan and its Prediction Approved and continue to `praxis-act`.

## Outputs

Prediction Assessment and the reason for approval or rejection.

## Success Criteria

## Domain Alignment

## Related Skills

- praxis-start-or-resume
- praxis-decompose
- praxis-plan
- praxis-predict
- praxis-act
- praxis-analyze
- praxis-learn
- praxis-record

## Troubleshooting
