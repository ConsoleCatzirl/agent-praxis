---
name: praxis-plan
description: Create a Plan for a list of Tasks
---

# Skill: Praxis Plan

Determine an appropriate list of patterns and one-off skills, tools, and commands to address each current Task.

## Origin
Initial Implementation

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

If there are any existing Rejected Plans, review the reason for the rejection so that we can create a revised Plan.
Review the Patterns and their Confidence in `.praxis/tracking/{patterns,confidence}.md`.
Determine an optimal sequence of Patterns, creating new ones as needed, to address the current Tasks.
Document as one or more Plans, each with assigned Tasks using `.praxis/templates/plans-template.md`.

## Output

One or more Plans in `.praxis/state/plans.md`

## Success Criteria

Plans have been written to state

## Domain Alignment

## Related Skills

- praxis-start-or-resume
- praxis-decompose
- praxis-predict
- praxis-discern
- praxis-act
- praxis-analyze
- praxis-learn
- praxis-record

## Troubleshooting

