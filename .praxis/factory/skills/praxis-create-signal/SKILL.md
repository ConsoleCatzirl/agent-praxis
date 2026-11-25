---
name: praxis-create-signal
description: Add a Signal to `.praxis/tracking/signals/`, or revise one, from the signal template, and list it in `.praxis/tracking/signals.md`. Use when a reflection, introspection or Learn finds a part of the Flow that no Signal measures, or a Signal that measures it badly.
confidence: Low
complexity: Qualitative
implements:
  - Add or Refine a Signal
---

# Skill: Praxis Create Signal

Write the file of a Signal (a calibration or self-evaluation metric for the Flow) and its list entry, so that its metric is stated in a way a script can compute.

## Origin
Pattern: Add or Refine a Signal, whose first step was prose done by the agent (the pattern's own note called it a candidate skill). Written on 2026-11-22 so that every step of a Pattern names a factory product (Rule: Every Pattern Step MUST Name a Factory Product).

## Purpose
Keep each Signal one file with the template's sections, a metric that can be computed, and one entry in the list, so that the script that computes the Signals and `praxis-flow-learn` can read and fill it.

## When to Use
When a reflection, introspection or Learn finds a part of the Flow that no Signal measures, or a Signal that measures it badly. Run it as the first step of Pattern: Add or Refine a Signal. Not for recording a Signal's values: `praxis-flow-learn` writes those.

## How it Works
The skill checks whether the Signal exists, writes or revises its file from `.praxis/templates/signal-template.md` with a Metric a script can compute, and adds or updates its entry in `.praxis/tracking/signals.md`. The Pattern's next steps extend the script that computes the Signals (or, where there is none, a step of `praxis-flow-learn`) to compute the metric and check the result.

## Requirements
- A part of the Flow to measure, and why it matters.
- `.praxis/templates/signal-template.md`, `.praxis/tracking/signals.md` and `.praxis/tracking/signals/README.md` exist.

## Inputs
The Signal's name, what it describes, how it is measured, and what it is for; for a revision, the Signal and the reason.

## Procedure
1. Read `.praxis/templates/signal-template.md`, `.praxis/tracking/signals.md`, and the Signals that measure neighboring parts of the Flow (to avoid two Signals that read the same thing).
2. Look for the name in `.praxis/tracking/signals.md`. If it is listed, this is a revision: read its file and change only what the reason touches.
3. Write `.praxis/tracking/signals/${subject}-${measure}.md` (lowercase, hyphenated, like `outcomes-accurate.md`) from the template, with the template's headings in its order:
   - **Description**: what the Signal measures.
   - **Metric**: how it is computed, stated so that a script can compute it (for a mechanical metric, say what is counted and where the number is printed or written). A metric that needs judgement says so and names the skill that makes it.
   - **Purpose**: what it tracks and why, naming the domain items it serves (Rule, Value, Intention).
   - **Values**: `None yet: no run has been recorded in this project.` for a new Signal; `praxis-flow-learn` adds readings, newest first. Leave the readings of a revised Signal alone and say in Notes that its metric changed (a changed metric is comparable only from the change).
   - **Notes**: limits and cautions; `None.` when there are none.
4. Add or update the Signal's entry in `.praxis/tracking/signals.md` (`* [Name](./signals/${file}.md)`), keeping the list in alphabetical order by name.
5. Leave the computing of the metric to the next step of the Pattern (a script change, then the script that computes the Signals), and say in the Outcome which part of the Metric still has no script.

## Output
A new or revised Signal file in `.praxis/tracking/signals/` and its entry in `.praxis/tracking/signals.md`.

## Success Criteria
- The file has every section of the template, in its order, and none holds its bracketed prompt.
- The Metric can be computed by a named script or names the skill that judges it.
- The Signal is listed once, in alphabetical order, with a link that resolves.
- No other Signal's Values were changed.

## Domain Alignment

Aligned
- Value: Reliable Self-Knowledge
- Rule: Each Outcome MUST Be Compared With Its Prediction
- Intention: Improving With Each Run

Unaligned
- none known

## Related Skills

- praxis-refine-script
- praxis-flow-learn
- praxis-flow-introspect
- praxis-self-reflect

## Troubleshooting

### Issue: The Signal reads the same in every run

Identifying:
Its Values are equal across runs, so it does not discriminate.

Solution:
Revise its Metric or retire it with the user's consent; do not keep a Signal that cannot move.

### Issue: The metric needs judgement, not a script

Identifying:
No line a script could print gives the value.

Solution:
Name the skill that makes the judgement in the Metric, and say so in Notes; do not pretend a script computes it.

## Notes

Used first in the project this tree was lifted from; no use yet in this one.
