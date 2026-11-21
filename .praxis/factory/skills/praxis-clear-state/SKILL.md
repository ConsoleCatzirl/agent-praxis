---
name: praxis-clear-state
description: Clear previous praxis state
---

# Skill: Praxis Clear

Prepare a new Praxis Flow run by clearing out previous state in `.praxis/state/`.

## Origin
Initial Implementation

## Description
Remove any named Tasks, Plans, Predictions, Outcomes, and Analyses from state, keeping only header/stub files

## Purpose
Remove previous state in preparation for the next Flow iteration

## When to Use
After recording and reporting a Flow iteration, and occassionally abandoning state to start fresh.

## Requirements
State has been recorded and reported

## Inputs
None

## Procedure
1. If the current iteration is not complete, abort.
2. Summarize the Tasks and Plans for this iteration, this will be our git commit message.
3. Remove all items from `.praxis/state/*/${items}`.
4. Commit the removal with a description of the completed tasks and plans.

## Output
Empty state

## Success Criteria
No live iteration-specific state

## Domain Alignment

## Related Skills

- praxis-\*

## Troubleshooting
