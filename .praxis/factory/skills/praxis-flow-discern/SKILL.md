---
name: praxis-flow-discern
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
Compare expected outcomes with domain items to determine a verdict.

## Requirements

Created Prediction

## Inputs

Created Predicton

## Procedure

As each Prediction is created:
1. Review the lists of domain items.
2. For any items relevant to the Prediction or its Plan, review the details for that item.
3. Assess the expected outcomes from the Prediction for violations with the relevant domain items.
4. If any expected outcomes would be harmful, reject the Plan outright.
5. If any expected outcomes would be detrimental, send the Plan back `praxis-flow-plan` for revision.
6. If any Tasks for the Plan would not be completed by the expected outcomes, send the Plan back `praxis-flow-plan` for revision.
7. If there aren't any expected harmful or detrimental outcomes, and all listed Tasks would be completed, approve the Plan.

## Outputs

Prediction Assessment and the reason for approval or rejection.

## Success Criteria

## Domain Alignment

## Related Skills

- praxis-\*

## Troubleshooting
