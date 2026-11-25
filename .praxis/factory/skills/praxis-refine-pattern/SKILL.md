---
name: praxis-refine-pattern
description: Revise an existing pattern in `.praxis/factory/patterns/`, keeping its file, list entry, alignment, confidence row, lifecycle, and every document that states it consistent, and commit the change. Use when a pattern needs new wording, new evidence, a changed confidence, or to be abandoned.
confidence: Low
complexity: Qualitative
implements:
  - Refine a Praxis Component
---

# Skill: Praxis Refine Pattern

Change an existing pattern (an ordered list of factory products that compose to complete a kind of Task) without breaking its file, list, alignment, or lifecycle.

## Origin
Praxis Template

## Purpose
Revise a pattern one reason at a time, so that every change is justified, the confidence and stage follow `.praxis/lifecycles/evidenced-lifecycle.md` and `.praxis/lifecycles/confidence-lifecycle.md`, and nothing is left disagreeing with it.

## When to Use
When an Analysis, introspection, self-reflection, or the user shows that a pattern is wrong, unclear, out of date, in conflict with another item, or ready for a different confidence. Not for creating a pattern; use `praxis-create-pattern`.

## How it Works
The skill classifies the reason for the change, applies the smallest edit that addresses it, adjusts the confidence and stage only as the lifecycle allows, re-checks alignment with the other items, and commits. A stage move is made with `praxis-promote-evidenced`, which holds the evidence required for each move (Hypothesized to Evidenced, Evidenced to Established, any move to Challenged, and any move to Debunked).

## Requirements
- An existing pattern in `.praxis/factory/patterns.md`.
- A stated reason for the change, with its source: user statement, Analysis, introspection, or an observed contradiction.
- None beyond the evidence; tracking changes need no consent, but a Pattern a Plan depends on is changed through a revised Plan.

## Inputs
The pattern's name and the reason for the change, with any evidence.

## Procedure
1. Read the following files if they are not already in context: `.praxis/factory/patterns/${item-name}.md`, `.praxis/factory/patterns/README.md`, `.praxis/templates/pattern-template.md`, `.praxis/lifecycles/evidenced-lifecycle.md`, and `.praxis/lifecycles/confidence-lifecycle.md`.
2. Classify the reason, and handle it as follows:
   - **Wording or content**: edit only the sections that the reason touches. Content that changes the meaning of the pattern, not its phrasing, is a minor revision, and content that reverses it a major revision (`.praxis/glossary.md`, "Major revision").
   - **New evidence**: add it under Evidence Notes with where it came from (a Plan, Outcome, Analysis or user statement). Evidence from one Flow run counts once, however many times it was used in that run.
   - **Confidence change**: apply only a change that a path in the confidence lifecycle allows, and write the evidence for it in the file.
   - **Stage change**: use `praxis-promote-evidenced` and return here for the file and table updates.
   - **Abandonment**: a Debunked pattern stays in git history; follow the lifecycle's Cleared stage with the user's consent.
3. Check that no Plan in `.praxis/state/plans/` depends on the current procedure; if one does, revise that Plan instead of editing the Pattern under it.
4. Edit the file. The Procedure stays general prose, with no paths or product names. If the change adds or removes an implementing skill, change the skill's frontmatter `implements:` to match (`praxis-refine-skill`, or `praxis-create-skill` for a new skill); the Pattern keeps at least one (Rule: Every Pattern MUST Be Implemented by at Least One Skill). Update the `modified` timestamp with `date -Iseconds`, leave `created` alone, and keep every template heading.
5. If the change was a major revision of an item at Medium or higher, lower its confidence to what the lifecycle allows for a revised item (Low or Medium) unless the user directs otherwise.
6. Re-check Domain Alignment: every referenced item must still exist, and re-read the items that mention this pattern in their own alignment. Update any that no longer agree, and record a new contradiction as a contradiction, not as a silent edit.
7. Update the item's row in `.praxis/tracking/confidence/patterns.csv` (confidence,lifecycle,details,name) so it matches the file. When the confidence or stage changes, change the file and the row together, and make only a move the lifecycles give.
8. If the name changed, update the link in `.praxis/factory/patterns.md`.
9. Propagate the change when it altered what the pattern says or what it is called (not for a pure typo). Do this by search, not by memory:
   1. State the change in one sentence, with who decided it and when.
   2. Search the current tree for the old wording and its neighbors (inflections, synonyms, field names, the routes and callers that reach it, and the prose that states it, not only its syntax) across `.praxis/` (`flow.md`, `CLAUDE.md`, `README.md`, `glossary.md`, `lifecycles/`, `templates/`, `domains/`, `factory/`, `tracking/`; leave `state/` and git history alone, since they record what was true then). List each document and line. If the change is part of a Plan, run this search before the Plan is reviewed and name every line in the Plan; say in the Prediction that the list shows the places found, not that it is complete.
   3. Keep one definition: this pattern. Every other document says it in one line or points here.
   4. Change each other document with an exact replacement that fails if the old text is not there, so a stale or already-changed document is noticed and not skipped.
   5. Search again for the old wording; the result is empty except where history is kept on purpose. List what remains and why.
   6. Walk a case through the changed text: take a real instance (this run's own state files, or a past case) and follow the new wording step by step. Fix what the walk finds.
   7. Check that the list entry, template sections, statuses and alignment references still hold, that every Procedure step names a product, and that no check that passed before now fails.
10. Stage the change and run the checks that Pattern: Refine a Praxis Component requires before a commit (the checks above and the tests of any staged script); on a failure, fix the cause and check again, and do not commit until it passes. Then commit the file, the confidence row and the propagation edits as one logical change per concern with `git -C .praxis`, giving the reason and who decided it in the message. Record in the Outcome which documents were changed and which were left on purpose. The commit carries the trailer of its kind: `Revision: breaking` for a major revision, `Revision: feature` for a minor one, and `Revision: fix` or none for a patch (`.praxis/glossary.md`, "Major revision").

## Output
A revised pattern file, with its list entry, confidence row and neighbors consistent, and a commit.

## Success Criteria
- The change matches the stated reason and nothing more.
- Status and Confidence are a legal move in `.praxis/lifecycles/evidenced-lifecycle.md`.
- `grep -rn` finds no reference to a name that no longer exists, and a search for the old wording finds only history.
- A walked case follows the new wording without a gap.
- Every step of the Procedure names one factory product that exists, and none is written as prose (read each step to check).
- The `modified` timestamp changed and `created` did not.

## Domain Alignment

None recorded yet; the lists are still being populated.

## Related Skills

- praxis-create-pattern
- praxis-create-skill
- praxis-refine-skill
- praxis-promote-evidenced
- praxis-flow-learn
- praxis-flow-introspect
- praxis-flow-self-review

## Troubleshooting

### Issue: The reason is a single observation

Identifying:
The only support for the change is one Outcome or one remark.

Solution:
Record it under Evidence Notes and leave the content and confidence alone until it recurs independently, or the user directs the change.

### Issue: The change contradicts something the user stated directly

Identifying:
The pattern came from a direct user statement and the evidence argues against it.

Solution:
Do not weaken or remove it on the agent's authority. Present the evidence as thesis, antithesis, and a proposed synthesis, and let the user decide.

### Issue: The old wording is part of a record

Identifying:
The old wording appears in committed state, Outcomes, Analyses, or git history.

Solution:
Leave it: those say what was true when they were written. Name it in the list of what was left.

### Issue: A document states the change in different words

Identifying:
A search for the exact old text finds nothing, but another document says the same thing differently.

Solution:
Search for the neighbors of the wording (names, synonyms, field names), not only the exact text, and ask the user if two readings are possible.

### Issue: Other items depended on the old wording

Identifying:
A `grep -rn` of the name finds references in other items, Plans, or skills whose meaning changed.

Solution:
Update the references in the same commit when they are mechanical; otherwise create a Task for each, and say so in the Outcome.

### Issue: A step has no factory product

Identifying:
A changed step would be written as prose, or a step names no product.

Solution:
Do not write the prose into the Pattern. A mechanical step becomes a script (`praxis-create-script`); a step that needs judgement or instructions becomes a skill, new (`praxis-create-skill`) or an addition to an existing one (`praxis-refine-skill`). Then name that product in the step.
