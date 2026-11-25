---
name: praxis-refine-habit
description: Change an existing habit with the smallest edit that fits the reason, rerun it, and update its README and tracking row.
confidence: Low
---

# Skill: Praxis Refine Habit

## Origin
Written for this template as a mechanism of the factory, with no recorded use.

## Purpose
Keep a habit's steps, declared complexity and tracking row true to what it does now.

## When to Use
When a habit does not do what its README says, should do a little more, or a step would now need judgement.

## How it Works
The skill classifies the change, edits the README, reruns the sequence, adjusts the tracking row, and commits.

## Requirements
- An existing habit listed in `.praxis/factory/habits.md`, with its README.
- A stated reason for the change.

## Inputs
The habit's name and the reason for the change.

## Procedure
1. Read `.praxis/factory/habits/${habit}/README.md`, its row in `.praxis/tracking/confidence/habits.csv`, `.praxis/templates/habit-template.md` and `.praxis/lifecycles/factory-lifecycle.md`.
2. Classify the change: a fix (the habit does not do what its README says), an extension (add the fewest steps; if its Purpose would no longer fit in one sentence, create a second habit with `praxis-create-habit`), or a step that would need judgement (stop: that belongs in a skill).
3. Edit the README: the Procedure, then Complexity as the highest level of its steps (never above Structural), Interface, Tests, and the modified timestamp from `date -Iseconds`.
4. Run the sequence once as written and record the result under Tests.
5. Update the row in `.praxis/tracking/confidence/habits.csv` by hand, following `.praxis/lifecycles/confidence-lifecycle.md`: a change moves confidence only on recorded evidence.
6. Read each skill that names the habit and fix any step the change breaks.
7. Commit the habit, its row and any skill changed as one logical change, giving the reason in the message.

## Output
The changed habit, its tracking row, any skill that names it, and a commit.

## Success Criteria
- The change matches the stated reason and nothing more.
- The declared Complexity equals the highest of its steps.

## Domain Alignment

Aligned
- none known

Unaligned
- none known

## Related Skills

- praxis-create-habit

## Troubleshooting

### Issue: A step now needs judgement

Identifying:
The change adds a step whose input depends on judging the previous output.

Solution:
Stop, and write a skill that names the habit instead.
