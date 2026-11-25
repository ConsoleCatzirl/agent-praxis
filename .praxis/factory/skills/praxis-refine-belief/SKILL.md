---
name: praxis-refine-belief
description: Revise an existing belief in `.praxis/domains/beliefs/`, keeping its file, list entry, alignment, confidence row, lifecycle, and every document that states it consistent, and commit the change. Use when a belief needs new wording, new evidence, a changed confidence, or to be abandoned.
confidence: Low
complexity: Qualitative
---

# Skill: Praxis Refine Belief

Change an existing belief (a falsifiable statement developed through evidence and inference) without breaking its file, list, alignment, or lifecycle.

## Origin
Taken from the workspace's skill of the same name, without its run evidence; no recorded use on this branch.

## Purpose
Revise a belief one reason at a time, so that every change is justified, the confidence and stage follow `.praxis/lifecycles/evidenced-lifecycle.md` and `.praxis/lifecycles/confidence-lifecycle.md`, and nothing is left disagreeing with it.

## When to Use
When an Analysis, introspection, self-reflection, or the user shows that a belief is wrong, unclear, out of date, in conflict with another item, or ready for a different confidence. Not for creating a belief; use `praxis-create-belief`.

## How it Works
The skill classifies the reason for the change, applies the smallest edit that addresses it, adjusts the confidence and stage only as the lifecycle allows, re-checks alignment with the other items, and commits. A stage move is made with `praxis-promote-evidenced`, which holds the evidence required for each move (Hypothesized to Evidenced, Evidenced to Established, any move to Challenged, and any move to Debunked).

## Requirements
- An existing belief in `.praxis/domains/beliefs.md`.
- A stated reason for the change, with its source: user statement, Analysis, introspection, or an observed contradiction.
- The owner's request for the change, or the agent's case-by-case judgement that it may be made now (`CLAUDE.md`, "Domain and Tracking Changes").

## Inputs
The belief's name and the reason for the change, with any evidence.

## Procedure
1. Read the following files if they are not already in context: `.praxis/domains/beliefs/${item-name}.md`, `.praxis/domains/beliefs/README.md`, `.praxis/templates/belief-template.md`, `.praxis/lifecycles/evidenced-lifecycle.md`, and `.praxis/lifecycles/confidence-lifecycle.md`.
2. Classify the reason, and handle it as follows:
   - **Wording or content**: edit only the sections that the reason touches. Content that changes the meaning of the belief, not its phrasing, counts as a minor revision, and content that reverses it as a major revision (`.praxis/glossary.md`, "Major revision").
   - **New evidence**: add it under Evidence Notes with where it came from (a Plan, Outcome, Analysis or user statement). Evidence from one Flow run counts once, however many times it was used in that run.
   - **Confidence change**: apply only a change that a path in the confidence lifecycle allows, and write the evidence for it in the file.
   - **Stage change**: use `praxis-promote-evidenced` and return here for the file and table updates.
   - **Abandonment**: a Debunked belief stays in git history; follow the lifecycle's Cleared stage, judged case by case like any change (step 3).
3. Judge, case by case, whether to make the change now or to propose it to the owner first (`CLAUDE.md`, "Domain and Tracking Changes"); to propose it, stop here and name it in the `praxis-flow-learn` review.
4. Edit the file. Update the `modified` timestamp with `date -Iseconds`, leave `created` alone, and keep every template heading.
5. If the change was a major revision of an item at Medium or higher, lower its confidence to what the lifecycle allows for a revised item (Low or Medium) unless the user directs otherwise.
6. Re-check Domain Alignment: every referenced item must still exist, and re-read the items that mention this belief in their own alignment. Update any that no longer agree, and record a new contradiction as a contradiction, not as a silent edit.
7. Update the item's row in `.praxis/tracking/confidence/beliefs.csv` (confidence,lifecycle,details,name) so it matches the file. When the confidence or stage changes, the `promote` script of the workspace (not on this branch: do the step by hand) writes the file and the row together and refuses a move the lifecycles do not give.
8. If the name changed, update the link in `.praxis/domains/beliefs.md`.
9. Propagate the change when it altered what the belief says or what it is called (not for a pure typo). Do this by search, not by memory:
   1. State the change in one sentence, with who decided it and when.
   2. Search the current tree for the old wording and its neighbors (inflections, synonyms, field names, the routes and callers that reach it, and the prose that states it, not only its syntax) across `.praxis/` (`flow.md`, `CLAUDE.md`, `README.md`, `glossary.md`, `lifecycles/`, `templates/`, `domains/`, `factory/`, `tracking/`; leave `state/` and git history alone, since they record what was true then). List each document and line. If the change is part of a Plan, run this search before the Plan is reviewed and name every line in the Plan; say in the Prediction that the list shows the places found, not that it is complete.
   3. Keep one definition: this belief. Every other document says it in one line or points here.
   4. Change each other document with an exact replacement that fails if the old text is not there, so a stale or already-changed document is noticed and not skipped.
   5. Search again for the old wording; the result is empty except where history is kept on purpose. List what remains and why.
   6. Walk a case through the changed text: take a real instance (this run's own state files, or a past case) and follow the new wording step by step. Fix what the walk finds.
   7. Run the `checks` script of the workspace (not on this branch: do the step by hand): it must exit 0 (hygiene, tmplcheck and statuscheck are among its checks).
10. Commit the file, the confidence row and the propagation edits as one logical change per concern with `git`, giving the reason and who decided it in the message. Record in the Outcome which documents were changed and which were left on purpose.

## Output
A revised belief file, with its list entry, confidence row and neighbors consistent, and a commit.

## Success Criteria
- The change matches the stated reason and nothing more.
- Status and Confidence are a legal move in `.praxis/lifecycles/evidenced-lifecycle.md`.
- `grep -rn` finds no reference to a name that no longer exists, and a search for the old wording finds only history.
- A walked case follows the new wording without a gap.
- The `modified` timestamp changed and `created` did not.

## Domain Alignment

None recorded yet; the domain lists are still being populated.

## Related Skills

- praxis-create-belief
- praxis-promote-evidenced
- praxis-flow-learn
- praxis-flow-introspect
- praxis-self-reflect

## Troubleshooting

### Issue: The reason is a single observation

Identifying:
The only support for the change is one Outcome or one remark.

Solution:
Record it under Evidence Notes and leave the content and confidence alone until it recurs independently, or the user directs the change.

### Issue: The change contradicts something the user stated directly

Identifying:
The belief came from a direct user statement and the evidence argues against it.

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
