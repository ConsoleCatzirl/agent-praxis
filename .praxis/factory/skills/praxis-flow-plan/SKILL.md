---
name: praxis-flow-plan
description: Create a Plan for a list of Tasks
---

# Skill: Praxis Plan

Determine an appropriate list of patterns and one-off skills, tools, and commands to address each current Task.

## Origin
Praxis Template

## Purpose
Establish a sequence of Patterns to fulfill a set of Tasks

## When to Use
After decomposing a prompt into Tasks, before anticipating a prediction

## How it Works

## Requirements

Tasks decomposed from a user prompt

## Inputs

Tasks in `.praxis/state/tasks.md`

## Procedure

1. Read each Task in `.praxis/state/tasks/${task}.md`.
2. For any Identified Trivial Tasks:
  1. Create a Bypassed Plan listing all of the Identified Trivial Tasks
  2. Create a Bypassed Prediction for the Bypassed Plan
  3. Promote the Identified Trivial Tasks to Approved.
  4. Complete the Identified Trivial Tasks.
  5. Create a Bypassed Outcome for the Identified Trivial Tasks and mark them Completed
3. Read the following files if the are not already in context:
  - `.praxis/{domains,factory}/*md`
2. Read any existing Plans in `.praxis/state/plans/`, noting the Plan status and the Tasks it completes.
4. For any Identified Tasks:
  1. Review the Task for any major violations with domain items, if any are found then mark the Task Rejected with a Note naming the reason, otherwise mark it Approved.
5. Create a Bypassed Plan for any Approved Trivial Tasks.
6. For any other Approved Tasks, current or pre-existing, group the Tasks based on dependency and similarity.
7. For each group of Tasks, create a Plan to complete those Tasks:
  1. A Rejected Plan covering the same Tasks can be informative.
  2. The Procedure for a Plan is an ordered list of Patterns from the factory.
  3. The Procedure for a Pattern is an ordered list of factory products, including other Patterns.
  4. Identify appropriate existing Patterns to complete the Tasks for this Plan, prioritizing based on confidence.
  5. If no existing Pattern can address a current Task:
    1. If an existing Pattern can address the Task with minimal change to the Pattern, preserving the original purpose for the Pattern, add that minimal change to the Plan.
    2. If no existing Pattern is appropriate for modification, create a new Pattern to address the issue:
      1. If existing factory products can be combined into a Pattern to address this Task, create that pattern in the factory and use it in this Plan.
      2. If new factory products need to be created to address the Task, create a new Task for creating the factory products in a new Plan this Plan will depend on.
  6. Create the Plan from `.praxis/templates/plan-template.md` and add an entry to `.praxis/state/plans.md`.

## Output

One or more Plans in `.praxis/state/plans.md`

## Success Criteria

Plans have been written to state

## Domain Alignment

## Related Skills

- praxis-\*

## Troubleshooting

