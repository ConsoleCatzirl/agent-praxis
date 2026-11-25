---
name: praxis-create-lifecycle
description: Write a new lifecycle in `.praxis/lifecycles/` from the state or confidence lifecycle template, list it, check it, and name the scripts and documents that must learn it. Use when a new kind of item needs stages of its own.
confidence: Low
complexity: Qualitative
implements:
  - Create a Praxis Component
---

# Skill: praxis-create-lifecycle

## Origin
The owner, 2026-11-22: "create skills for creating lifecycles and templates", after the introspection lifecycle had to be written by hand (Plan Track Introspections as Items).

## Purpose
Give a new kind of item a lifecycle that is a valid state machine, agrees with the skills that move items through it, and is known to the scripts and documents that read lifecycles.

## When to Use
When a Plan adds a kind of item with stages of its own (as introspections did), or splits a lifecycle in two. To change an existing lifecycle, edit it, and every document that states its stages, instead.

## How it Works
The judgement is the stages: what each means, which skill moves an item in and out, and which moves need evidence. A check of the stages and the status words, by reading, tests the result; any scripts that hard-code lifecycles are changed through their own Tasks.

## Requirements
The kind of item, where its items live, and the skills that create and change them (existing, or planned in the same Plan).

## Inputs
The lifecycle's name, the items it covers, and their stages.

## Procedure
1. Read `.praxis/lifecycles/README.md`, the templates `.praxis/templates/state-lifecycle-template.md` and `.praxis/templates/confidence-lifecycle-template.md`, and one lifecycle of each kind (`.praxis/lifecycles/analysis-lifecycle.md`, `.praxis/lifecycles/factory-lifecycle.md`). Check that no lifecycle in `.praxis/lifecycles/` already covers the items; if one does, stop and change it instead.
2. Choose the template: the state template for items moved by skills alone (state, tracking records such as introspections), the confidence template for items whose stage follows confidence levels (domain items, factory products).
3. Choose the stages, each with a one-sentence meaning that no other stage shares. Write the Stage Flow (`New -> ...`; `New` and `Cleared` are implicit) so that every stage is reachable from New and can reach Cleared, and no edge exists that no skill or rule takes.
4. Write `.praxis/lifecycles/${name}-lifecycle.md` from the template: a paragraph saying what the items are and where they live; `## Stages`; `## Stage Flow`; and a `## Stage N: Name` section per stage, numbered from 1, with its description and its Entry Paths and Exit Paths. In a state lifecycle, each path names the skill that takes it in backticks (an existing skill directory in `.praxis/factory/skills/`), with its condition in parentheses; in a confidence lifecycle, each path is labelled with the confidence levels it allows, and the stage's `**Confidence:**` line lists them. Write who decided a rule and when, as the other lifecycles do.
5. Add the lifecycle to `.praxis/lifecycles/README.md` under the section for its kind (Domain, Factory, State, Tracking), with a one-line description; add a section if none fits.
6. Name it where its items are described: the README of the items' directory (for example `.praxis/tracking/README.md` or `.praxis/factory/<type>s/README.md`) and the skills that create and change the items.
7. Check that every stage is reachable from New and can reach Cleared, that each Stages list equals its Stage Flow, and that the status phrases in skills name real stages; none may fail. A finding that names a skill that does not exist yet is expected only when that skill is created in the same Plan; commit only once it exists.
8. Look for any script or check on the project that must learn the lifecycle (one that handles the items in `.praxis/state/`, one that moves confidence between stages, one that checks status words, or one that checks that each item's Status is a stage of its lifecycle), and write a Task for each rather than editing them here. Search the project's scripts for the word "lifecycle" for any other. A branch with no scripts has nothing to do in this step.
9. Walk one item through the lifecycle from New to Cleared, naming the skill at each move, and fix any move that no skill takes.
10. Stage the lifecycle and the README changes, check that the lifecycle and the README read correctly, and commit with `git -C .praxis` only when it passes.

## Output
A lifecycle in `.praxis/lifecycles/`, listed in `.praxis/lifecycles/README.md` and named where its items are described; Tasks for the scripts that must learn it.

## Success Criteria
- Every stage is reachable from New and can reach Cleared, each Stages list equals its Stage Flow, and no status phrase names a stage that does not exist.
- Every stage has a meaning of its own and a skill that enters and leaves it; the walk reaches Cleared.
- Each script that hard-codes lifecycles and must learn this one has a Task.

## Domain Alignment

Aligned
- Rule: Praxis Records MUST Conform to Their Templates and Lifecycles
- Value: Reliability
- Practice: Walk a Case Through a Changed Rule Before Calling It Done

Unaligned
- none known

## Related Skills

- praxis-create-template
- praxis-create-skill
- praxis-refine-script

## Troubleshooting

### Issue: A stage cannot reach Cleared

Identifying:
A stage cannot reach Cleared.

Solution:
Add the move that ends an item's life (often on the owner's word, with git keeping the item), or merge the stage into one that can.

## Notes

None.
