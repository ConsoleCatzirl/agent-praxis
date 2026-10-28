---
name: praxis-start-or-resume
description: Prompt entry-point for determing current Flow stage
---

# Skill: Praxis Start or Resume

## Origin
Initial Implementation

## Purpose
Resume previous Tasks or start new ones

## When to Use
Immediately after receiving a prompt from the user

## How it Works
Review current state to determine the current phase and stage

## Requirements
User prompt

## Input
User prompt and current state

## Procedure

First match of:
- If all current live state is empty, continue to `praxis-decompose`.
- If all current live state is in its final status state and there are no uncommitted changes to `.praxis/`, then clear the state using `praxis-clear` and continue to `praxis-decompose`.
- If the only defined state are Tasks, continue to `praxis-plan`.
- If the only defined state are Tasks and Plans, continue to `praxis-predict`.
- If the only defined state are Tasks, Plans, and Predictions, and at least one Prediction or Plan is neither Approved nor Rejected, then continue to `praxis-discern`.
- If at least one Plan is Approved and all other Plans are either Approved or Rejected, continue to `praxis-act`.
- If all Plans are Rejected, continue to `praxis-analyze`.
- If all Plans have actualized Outcomes, continue to `praxis-analyze`.
- If all actualized Plans and Outcomes have associated Analyses, continue to `praxis-learn`.
- If all Analyses are Processed, continue to `praxis-record`.

Any other cases should be evaluated case-by-case.

## Output
None

## Success Criteria

The next Flow stage is clearly identified

## Domain Alignment

## Related Skills

- praxis-start-or-resume
- praxis-plan
- praxis-predict
- praxis-discern
- praxis-act
- praxis-analyze
- praxis-learn
- praxis-record

## Troubleshooting
