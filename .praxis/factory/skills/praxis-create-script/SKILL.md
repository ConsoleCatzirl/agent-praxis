---
name: praxis-create-script
description: Create new scripts in `.praxis/factory/scripts/`
---

# Skill: Create Script

Create a new script in the factory

## Origin
Initial Implementation

## Description
Implement scripts, right-sized to complexity.

## Purpose
Create new scripts in the factory

## When to Use
When creating a new script in the factory.

## Requirements
A need for a new script.

## Inputs
None

## Procedure
1. Identify the complexity level of the script.
2. Identify an ideal implementation for the script:
  - **Regex**: prioritize `.sed` scripts, combined with `grep`, `find`, `head`, `tail`, `cut`, `tr`, `sort`, etc.; Python solutions can use `pythonsed` to re-use `.sed` scripts.
  - **Mechanical**: Prioritize shell scripts with compound statemens, process redirection, and process substitution for glue code, and Python for shared libraries.
  - **Structural**: Prioritize Python for the use of data structures, using `numpy` and `pandas` for advanced cases.

## Output
Empty state

## Success Criteria
No live iteration-specific state

## Domain Alignment

## Related Skills

- praxis-\*

## Troubleshooting
