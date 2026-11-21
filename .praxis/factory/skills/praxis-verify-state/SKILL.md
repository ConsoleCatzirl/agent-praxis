---
name: praxis-verify-state
description: Verify current praxis state
---

# Skill: Praxis Verify State

Determine the state of the current flow iteration.

## Origin
Initial Implementation

## Description
Read the contents of `.praxis/state/` and report on its state.

## Purpose
Verify understanding of the current iteration state.

## When to Use
Iteration state needs to be confirmed.

## Requirements
None

## Inputs
None

## Procedure

1. Read the Status of each state domain item, and if there aren't any then report that state is cleared.
2. If any of the following verifications fail, stop and provide a summary of in-progress Tasks and Plans.
3. Verify every Task is Completed or Rejected.
4. Verify every Plan is Completed or Bypassed.
5. Verify every Plan has a Prediction.
6. Verify every Prediction is Analyzed or Bypassed.
7. Verify every Prediction has an Outcome and an Analysis.
8. Verify every Outcome is Analyzed or Bypassed.
9. Verify every Analysis is Processed or Bypassed.
10. Verify all changes to `.praxis/` are committed.
11. Report that the current iteration is verified complete.

## Output
Current state of Tasks and Plans.

## Success Criteria
No live iteration-specific state

## Domain Alignment

## Related Skills

- praxis-\*

## Troubleshooting
