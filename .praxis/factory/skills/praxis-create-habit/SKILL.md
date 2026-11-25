---
name: praxis-create-habit
description: Create a new habit in `.praxis/factory/habits/`, an ordered list of scripts, hooks, tools or other habits at Structural or below, with its list entry and tracking row.
confidence: Low
---

# Skill: Praxis Create Habit

## Origin
Written for this template as a mechanism of the factory, with no recorded use.

## Purpose
Give a recurring sequence of deterministic products one name, a tracked confidence and a checked complexity level, so that skills run it the same way every time.

## When to Use
When the same sequence of scripts, hooks, tools or habits recurs in the steps of skills or in the Plans of several runs, or a skill being written needs one. A sequence that needs judgement between its steps is a skill, not a habit.

## How it Works
The skill checks that the habit is needed and deterministic, writes its README from the habit template, adds its list entry and tracking row by hand, runs the sequence once, and commits.

## Requirements
- The sequence: every step a script, hook, tool or habit that exists.
- `.praxis/templates/habit-template.md`, `.praxis/factory/habits/README.md` and `.praxis/lifecycles/factory-lifecycle.md` have been read.

## Inputs
The habit's name, its steps, and the skills or runs where the sequence recurs.

## Procedure
1. Read `.praxis/templates/habit-template.md`, `.praxis/factory/habits/README.md`, `.praxis/factory/habits.md` and `.praxis/lifecycles/factory-lifecycle.md`.
2. Check `.praxis/factory/habits.md` for a habit with the same name or the same steps. If one exists, stop and use `praxis-refine-habit`.
3. Check every step: it names a script, hook, tool or habit that exists, never a skill, an agent or a Pattern, and nothing between two steps needs judgement. If a step needs judgement, stop: the sequence belongs in a skill, which may name a smaller habit.
4. Create `.praxis/factory/habits/${habit}/README.md` from the template: both timestamps from `date -Iseconds`, Status `Unstable`, Confidence `Low`, and Complexity the highest level of its steps (Regex, Mechanical or Structural, never Qualitative); write Purpose, Origin, Procedure (one numbered step per product, by type and path), Interface, Tests, Conditions for Revision and Domain Alignment.
5. By hand, add the habit to `.praxis/factory/habits.md` in alphabetical order, and a row to `.praxis/tracking/confidence/habits.csv` with `Low`, `Unstable` and a run count of 0.
6. Run the sequence once as written and record the result under Tests; fix any step that cannot be run as written.
7. Change each skill whose steps run the sequence to name the habit by path.
8. Check by hand that the declared Complexity equals the highest of the steps, and commit the habit, its list entry, its row and the skills that now name it as one logical change.

## Output
A new habit under `.praxis/factory/habits/`, its list entry and tracking row, the skills that name it, and a commit.

## Success Criteria
- Every step names a script, hook, tool or habit that exists, and none needs judgement.
- The declared Complexity equals the highest of its steps and is not above Structural.

## Domain Alignment

Aligned
- none known

Unaligned
- none known

## Related Skills

- praxis-refine-habit
- praxis-create-skill

## Troubleshooting

### Issue: The sequence needs a decision between steps

Identifying:
A step's input depends on reading or judging the previous step's output.

Solution:
Split it: the deterministic runs become habits, and a skill holds the decision and names the habits.
