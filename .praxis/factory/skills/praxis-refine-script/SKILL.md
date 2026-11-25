---
name: praxis-refine-script
description: Modify an existing script in `.praxis/factory/scripts/` with the smallest change that fits the reason, retest it, update its README and confidence row, and commit. Use when a script's behavior needs fixing or extending.
confidence: Low
complexity: Qualitative
---

# Skill: Praxis Refine Script

Iteratively improve an existing script (any programmatic product that is not an agent hook or an MCP tool).

## Origin
Taken from the workspace's skill of the same name, without its run evidence; no recorded use on this branch.

## Purpose
Change a script while keeping it tested, documented, and honestly tracked, so that its confidence reflects what it does now.

## When to Use
When an Outcome, Analysis, introspection, or the user shows that a script is wrong, incomplete, or no longer right-sized. Not for adding a new script; use `praxis-create-script`. A script is any programmatic product that is not an agent hook or an MCP tool, a git hook included.

## How it Works
The skill classifies the change, makes the smallest edit, re-runs the script's tests, updates its README, and adjusts the lifecycle and confidence in `.praxis/tracking/confidence/scripts.csv` by the factory lifecycle: a major revision (`.praxis/glossary.md`, "Major revision") lowers its confidence one level (High to Medium) and keeps its stage (the hysteresis at Medium), and its current plan count restarts with the new revision.

## Requirements
- An existing script listed in `.praxis/factory/scripts.md`, with its README.
- A stated reason for the change.

## Inputs
The script's name and the reason for the change.

## Procedure
1. Read the following files if they are not already in context: `.praxis/factory/README.md`, `.praxis/factory/scripts/${script}/README.md`, the script's own files, its row in `.praxis/tracking/confidence/scripts.csv`, and `.praxis/lifecycles/factory-lifecycle.md`.
2. If another factory product already addresses the reason, use it in the script instead of adding code to the script.
3. Classify the change:
   - **Fix** (the script does not do what its README says): correct it, and add a test that would have caught it.
   - **Extension** (it should do more): add the minimum; if the purpose would no longer fit in one sentence, create a second script instead.
   - **Complexity change**: if a change moves the script up a level (for example a sed script that now needs data structures), re-run the right-sizing from `praxis-create-script` and consider a rewrite instead of a patch.
4. If another factory product must change too, create a Task and a Plan for that change instead of editing it here.
5. Make the change, then re-run the script's recorded tests. Report any test that fails; do not weaken a test to make it pass.
6. Update the README (`.praxis/templates/factory-product-template.md`; refresh `modified`, Status, Confidence): purpose, interface or behavior, tests, and conditions for revision.
7. Update the row in `.praxis/tracking/confidence/scripts.csv` (`script,confidence,lifecycle,…,current-plan-count,total-plan-count,version`): When the confidence or stage changes, the `promote` script of the workspace (not on this branch: do the step by hand) writes the file and the row together and refuses a move the lifecycles do not give.
   - A major revision of a script at High lowers it to Medium (a minor or patch revision changes no confidence); it stays Stable, since the stage changes only when confidence leaves Medium (factory lifecycle).
   - An Unstable script stays Unstable; lower its confidence one level if the change was a fix for a harmful outcome (see `.praxis/lifecycles/confidence-lifecycle.md`).
   - Leave the plan and revision counts to `plan-counts.py` (Learn writes them from history): this change, once committed, raises its version by its kind, and only a major revision resets its current count.
8. Stage the change and run the `pre-commit-checks` script of the workspace (not on this branch: do the step by hand) (the checks and the staged scripts' tests that Pattern: Refine a Praxis Component requires before a commit); on a failure, fix the cause and run it again, and do not commit until it passes. Then commit the change, the README, and the tracking row as one logical change with `git`, giving the reason in the message. The commit carries the trailer of its kind: `Revision: breaking` for a major revision, `Revision: feature` for a minor one, and `Revision: fix` or none for a patch (`.praxis/glossary.md`, "Major revision").

## Output
A modified script, retested, with an updated README and confidence row, and a commit.

## Success Criteria
- The change matches the stated reason and nothing more.
- The script's tests pass, and a fix has a new test.
- The README and tracking row agree with the script.
- The lifecycle and confidence are a legal move in `.praxis/lifecycles/factory-lifecycle.md`.

## Domain Alignment

None recorded yet; the domain lists are still being populated.

## Related Skills

- praxis-create-script
- praxis-promote-factory
- praxis-flow-analyze
- praxis-flow-learn

## Troubleshooting

### Issue: Callers depend on the old behavior

Identifying:
`grep -rn` of the script's name in `.praxis/` and `.claude/` finds users that the change would break.

Solution:
Keep the old behavior behind the old interface, or create a Task and Plan to update each caller in the same commit.

### Issue: The change is larger than a refinement

Identifying:
The purpose no longer fits in one sentence, or most of the script is being rewritten.

Solution:
Create a new script with `praxis-create-script`, and retire the old one through the factory lifecycle with the user's consent.
