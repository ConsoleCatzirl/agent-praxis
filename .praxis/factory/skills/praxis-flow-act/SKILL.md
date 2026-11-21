---
name: praxis-flow-act
description: Perform an approved Plan and record the Outcome
---

# Skill: Praxis Act

Perform an approved Plan and record the Outcome 

## Origin
Initial Implementation

## Purpose
Actualize (perform or act on) the Plan

## When to Use
When a Plan and its Prediction are Approved, before the Reflect phase

## How it Works
Follow the Procedures in any Approved Plans.

## Requirements

Approved or Bypassed Plan and related Prediction

## Inputs

Approved or Bypassed Plan

## Procedure

1. Perform any Bypassed Plans to complete their Trivial Tasks.
2. Review any Approved Plans to determine an appropriate order.
2. For each Approved Plan, perform the Plan's procedure.
3. As each Approved Plan completes:
  1. Create a new Outcome from `.praxis/templates/outcome-template.md` in `.praxis/state/outcomes/` from the results.
  2. Mark the Plan's Prediction Actualized.
  3. Mark the Plan's Tasks Completed.
  4. Mark the Plan Completed.
  5. Summarize the Outcome.

## Output

An Outcome for each Plan actualized.

## Success Criteria

An Outcome is documented for each Plan, and all Tasks are Completed

## Domain Alignment

## Related Skills

- praxis-\*

## Troubleshooting
