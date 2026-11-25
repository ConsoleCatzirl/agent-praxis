---
name: praxis-install-skill
description: Install a skill by moving it from `.praxis/factory/skills/` to `.claude/skills/${skill}` and recording it in `.praxis/factory/installs.yaml`, or uninstall it by moving it back.
confidence: Low
---

# Skill: Praxis Install Skill

## Origin
Written for this template as a mechanism of the factory, with no recorded use.

## Purpose
Make a skill available to the agent only when the install lifecycle says its confidence supports it, and keep one record of what is installed.

## When to Use
When a skill's confidence reaches the level the install lifecycle gives (High; Medium for a `praxis-flow-*` skill), or falls to None or the skill is Retired.

## How it Works
The skill checks the skill's confidence against `.praxis/lifecycles/install-lifecycle.md`, moves the directory with `git mv` so nothing is left behind, and updates `installs.yaml`.

## Requirements
- The skill's directory exists in `.praxis/factory/skills/` (to install) or in `.claude/skills/${skill}` (to uninstall).
- `.praxis/lifecycles/install-lifecycle.md` has been read.

## Inputs
The skill's name, and whether to install or uninstall it.

## Procedure
1. Read `.praxis/lifecycles/install-lifecycle.md` and `.praxis/factory/installs.yaml`.
2. Check the skill's confidence against the lifecycle's entry paths (to install) or exit paths (to uninstall); if the lifecycle does not give the move, stop and say why.
3. To install, run `git mv .praxis/factory/skills/${skill} .claude/skills/${skill}` from the repository root, so that nothing is left in `.praxis/factory/skills/`, and add `  ${skill}: .claude/skills/${skill}` under `skills:` in `.praxis/factory/installs.yaml`.
4. To uninstall, run the move the other way and remove the skill's line from `installs.yaml`.
5. Check by hand that the directory exists in exactly one of the two places, that `installs.yaml` names it exactly when it is in `.claude/skills/${skill}`, and that each document that names the skill's path still resolves.
6. Commit the move and `installs.yaml` as one logical change, naming the skill and the confidence that allowed it.

## Output
The skill's directory at its new location, `installs.yaml` updated, and a commit.

## Success Criteria
- The skill is in exactly one of `.praxis/factory/skills/` and `.claude/skills/${skill}`.
- `installs.yaml` records it if and only if it is installed.

## Domain Alignment

Aligned
- none known

Unaligned
- none known

## Related Skills

- praxis-promote-factory
- praxis-refine-skill

## Troubleshooting

### Issue: The skill is in both places

Identifying:
A copy was made instead of a move.

Solution:
Remove the copy that the install lifecycle says should not hold it, and fix `installs.yaml`.
