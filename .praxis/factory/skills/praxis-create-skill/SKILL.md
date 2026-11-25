---
name: praxis-create-skill
description: Create a new skill in `.praxis/factory/skills/` from the skill template, with its tracking row and list entry, and commit it. Use when a Plan needs a procedure the agent follows, usually a qualitative one that no existing skill covers.
confidence: Low
complexity: Qualitative
---

# Skill: Praxis Create Skill

Create a new skill in the factory.

## Origin
Taken from the workspace's skill of the same name, without its run evidence; no recorded use on this branch.

## Purpose
Add a skill that is needed, correctly named, written from the template, tracked at Unstable and Low, and never linked into use before it has earned confidence.

## When to Use
When `praxis-flow-plan` finds that a Task needs qualitative judgment and no existing skill or Pattern covers it. If the procedure is mechanical, structural, or a regex, create a script with `praxis-create-script` instead, and let a skill call the script (see "Factory Products and Complexity Levels" in `.praxis/factory/README.md`). It is also how a Pattern is implemented: every Pattern has at least one skill that carries out its general prose with specific steps for a situation (Rule: Every Pattern MUST Be Implemented by at Least One Skill). A skill's steps may name any factory product, habits especially, and may be prose. Such a skill may need no judgement, and then declares a level below Qualitative.

## How it Works
The skill checks that the skill is needed, writes `SKILL.md` from `.praxis/templates/skill-template.md` in a directory whose name equals the skill's `name`, lists it, and records it in `.praxis/tracking/confidence/skills.csv`. It does not link the skill into `.claude/skills/<name>/`; that is promotion (`praxis-promote-factory`).

## Requirements
- A Task or Plan that needs the skill.
- A name that is not already in `.praxis/factory/skills.md`.
- `.praxis/templates/skill-template.md`, `.praxis/factory/README.md`, and `.praxis/lifecycles/factory-lifecycle.md` have been read.

## Inputs
The purpose, the trigger (when it should run), and the model and effort the skill is expected to need; if the skill is written for a step of a Pattern, that Pattern and step.

## Procedure
1. Read the following files if they are not already in context: `.praxis/templates/skill-template.md`, `.praxis/factory/README.md`, `.praxis/factory/skills/README.md`, `.praxis/factory/skills.md`, and `.praxis/lifecycles/factory-lifecycle.md`.
2. Check `.praxis/factory/skills.md` and the directories in `.praxis/factory/skills/` for the name and for a skill with the same purpose. If one exists, stop and use `praxis-refine-skill`.
3. Judge whether the procedure needs qualitative assessment. Move every mechanical step into a script (existing, or new via `praxis-create-script`) and have the skill call it.
4. Create `.praxis/factory/skills/${skill}/SKILL.md` and `.praxis/factory/skills/${skill}/references/README.md`. The directory name, the `name:` in the frontmatter, and the name used by other skills must be identical.
5. Write `SKILL.md` from the template with the second of the template's two frontmatter blocks (`.praxis/templates/README.md`: the first describes the template and is not copied) holding `name`, `description` (what it does and when to use it, in one or two sentences), `confidence: Low`, `complexity:`, the highest level the skill's steps need, with the products it runs, and `implements:`, the Patterns it implements (a block list; leave it out if none) (`.praxis/state/README.md`, "Complexity Levels"; Qualitative only when a step needs judgement), then every template section in order. In Procedure, number the steps, name the files each step reads or writes by path, and say what to do when a step fails. In Output and Success Criteria, describe this skill's results, not another skill's.
6. In `references/README.md` list the files that support the skill (examples, checklists), or say there are none.
7. Register the skill with the `add-item` script of the workspace (not on this branch: do the step by hand): it adds the skill to `.praxis/factory/skills.md` in alphabetical order with its description, and a row to `.praxis/tracking/confidence/skills.csv` (`skill,model,effort,complexity,confidence,lifecycle,…,current-plan-count,total-plan-count,version`) at `Unstable`, `Low`, the frontmatter's complexity, plan counts `0` and revision count `1`. If it refuses, fix what it names (usually the frontmatter `name`) and run it again.
8. Dry-run the procedure once against a real or imagined Task and fix any step that cannot be followed as written.
9. If the skill implements a Pattern, add it to the Pattern's Implementing Skills (the skill that refines Patterns (not on this branch), or the skill that creates Patterns (not on this branch) for a new Pattern), and run the `complexitycheck` script of the workspace (not on this branch: do the step by hand): it must report no finding.
10. Commit the skill, its list entry, its tracking row, and the Pattern that lists it as one logical change with `git`.

## Output
A new skill directory under `.praxis/factory/skills/`, its list entry, a tracking row at Unstable and Low, and a commit.

## Success Criteria
- A reader with only `SKILL.md` and the files it names can follow the procedure.
- The directory name equals the frontmatter `name`, and the frontmatter `confidence` equals the tracking row.
- No template section is left with its bracketed prompt, and the Output and Success Criteria belong to this skill.
- The skill is not installed in `.claude/skills/<name>/`: it is installed only at its install level, by promotion (`.praxis/factory/skills/README.md`, "Installing a Skill").
- If the skill implements a Pattern, the Pattern lists it, its `implements:` names the Pattern, and the skill's Complexity is the highest level of the products its steps name.

## Domain Alignment

None recorded yet; the domain lists are still being populated.

## Related Skills

- praxis-refine-skill
- praxis-create-pattern
- praxis-refine-pattern
- praxis-create-script
- praxis-promote-factory
- praxis-flow-plan

## Troubleshooting

### Issue: The skill is mostly mechanical

Identifying:
Most steps are deterministic commands with no judgment.

Solution:
Write the script, and keep only the qualitative remainder in the skill.

### Issue: The skill duplicates part of a Flow skill

Identifying:
Its procedure repeats steps of a `praxis-flow-*` skill.

Solution:
Call that skill from this one, or propose the change to it through `praxis-refine-skill`.
