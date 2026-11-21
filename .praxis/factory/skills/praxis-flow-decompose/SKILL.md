---
name: praxis-flow-decompose
description: Decompose user prompt into tasks
---

# Skill: Praxis Decompose

Decompose the user prompt into a list of Tasks.

## Origin
Initial Implementation

## Purpose

Create Tasks based on the user prompt.

## When to Use

When a user submits a prompt, before any action is taken.

## How it Works

## Requirements

Coherent user prompt

## Input

Coherent user prompt

## Procedure

1. Read the following files if they aren't already in context:
  - `.praxis/state/README.md`
  - `.praxis/factory/README.md`
2. Identify all Tasks contained in the user prompt, asking the user for any needed clarity.
3. Create an item in `.praxis/state/tasks/` for each Identified Task using the template `.praxis/template/task-template.md`.

## Output

One or more Identified Tasks

## Success Criteria

All Tasks inferred from the user prompt are written to state.

## Domain Alignment

## Related Skills

- praxis-\*

## Troubleshooting

