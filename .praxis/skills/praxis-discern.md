---
name: praxis-discern
description: Determine whether on not act on a plan
---

# Skill: Praxis Discern

Review a Plan's Prediction and determine whether to act, alter the plan, or abort.

## Origin
Initial Implementation

## Purpose
Review Plans and their Predictions for approval or rejection.

## When to Use
After creating a Predicition, before performing its Plan

## How it Works

## Requirements

Created Prediction

## Inputs

Created Prediciton

## Procedure

For each Plan with a Prediction:
1. Review the anticipated outcomes for the Plan
2. If any anticipated outcomes would be harmful, mark the Plan and its Prediction Rejected
3. If any anticipated outcomes don't fulfill the Plan's Tasks, return to the Praxis Plan stage and create a new Plan with a new Prediction.
4. If there are no harmful anticipated outcomes and all respective Tasks would be completed, mark the Plan and its Prediction Approved

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
