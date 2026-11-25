---
name: praxis-refine-rule
description: Revise an existing rule in `.praxis/domains/rules/`, keeping its file, list entry, alignment, lifecycle, and every document that states it consistent, and commit the change. Use when a rule needs new wording, new rationale, a changed confidence, or to be abandoned.
confidence: Low
complexity: Qualitative
---

# Skill: Praxis Refine Rule

Change an existing rule (required agent behavior, stated with RFC 2119 keywords) without breaking its file, list, alignment, or lifecycle.

## Origin
Praxis Template

## Purpose
Revise a rule one reason at a time, so that every change is justified, the confidence and stage follow `.praxis/lifecycles/assertion-lifecycle.md` and `.praxis/lifecycles/confidence-lifecycle.md`, and nothing is left disagreeing with it.

## When to Use
When an Analysis, introspection, self-reflection, or the user shows that a rule is wrong, unclear, out of date, in conflict with another item, or ready for a different confidence. Not for creating a rule; use `praxis-create-rule`.

## How it Works
The skill classifies the reason for the change, applies the smallest edit that addresses it, adjusts the confidence and stage only as the lifecycle allows, re-checks alignment with the other items, and commits. A stage move is made with `praxis-promote-assertion`, which holds the evidence required for each move (Proposed to Asserted, Asserted to Questioned, Questioned back to Asserted or Proposed, and any move to Abandoned).

## Requirements
- An existing rule in `.praxis/domains/rules.md`.
- A stated reason for the change, with its source: user statement, Analysis, introspection, or an observed contradiction.
- The owner's request for the change, or the agent's case-by-case judgement that it may be made now (`CLAUDE.md`, "Domain and Tracking Changes").

## Inputs
The rule's name and the reason for the change, with any evidence.

## Procedure
1. Read the following files if they are not already in context: `.praxis/domains/rules/${item-name}.md`, `.praxis/domains/rules/README.md`, `.praxis/templates/rule-template.md`, `.praxis/lifecycles/assertion-lifecycle.md`, and `.praxis/lifecycles/confidence-lifecycle.md`.
2. Classify the reason, and handle it as follows:
   - **Wording or content**: edit only the sections that the reason touches. Content that changes the meaning of the rule, not its phrasing, counts as a minor revision, and content that reverses it as a major revision (`.praxis/glossary.md`, "Major revision").
   - **Confidence change**: apply only a change that a path in the confidence lifecycle allows, and write the evidence for it in the file.
   - **Stage change**: use `praxis-promote-assertion` and return here for the file and table updates.
   - **Abandonment**: an Abandoned rule stays in git history; follow the lifecycle's Cleared stage, judged case by case like any change (step 3).
3. Judge, case by case, whether to make the change now or to propose it to the owner first (`CLAUDE.md`, "Domain and Tracking Changes"); to propose it, stop here and name it in the `praxis-flow-learn` review.
4. Edit the file. Update the `modified` timestamp with `date -Iseconds`, leave `created` alone, and keep every template heading. A changed name keeps the form `X V Y`, and each exception keeps the form `X MAY Y if/when Z` (`.praxis/domains/rules/README.md`, Rule Template).
5. If the change was a major revision of an item at Medium or higher, lower its confidence to what the lifecycle allows for a revised item (Low or Medium) unless the user directs otherwise.
6. Re-check Domain Alignment: every referenced item must still exist, and re-read the items that mention this rule in their own alignment. Update any that no longer agree, and record a new contradiction as a contradiction, not as a silent edit.
7. No confidence table covers this domain; make sure the Status and Confidence in the file are the only record.
8. If the name changed, update the link in `.praxis/domains/rules.md`.
9. Propagate the change when it altered what the rule says or what it is called (not for a pure typo). Do this by search, not by memory:
   1. State the change in one sentence, with who decided it and when.
   2. Search the current tree for the old wording and its neighbors (inflections, synonyms, field names, the routes and callers that reach it, and the prose that states it, not only its syntax) across `.praxis/` (`flow.md`, `CLAUDE.md`, `README.md`, `glossary.md`, `lifecycles/`, `templates/`, `domains/`, `factory/`, `tracking/`; leave `state/` and git history alone, since they record what was true then). List each document and line. If the change is part of a Plan, run this search before the Plan is reviewed and name every line in the Plan; say in the Prediction that the list shows the places found, not that it is complete.
   3. Keep one definition: this rule. Every other document says it in one line or points here.
   4. Change each other document with an exact replacement that fails if the old text is not there, so a stale or already-changed document is noticed and not skipped.
   5. Search again for the old wording; the result is empty except where history is kept on purpose. List what remains and why.
   6. Walk a case through the changed text: take a real instance (this run's own state files, or a past case) and follow the new wording step by step. Fix what the walk finds.
   7. Check that the list entry, template sections, statuses and alignment references still hold, that the rule's name and any exception have their form, and that no check that passed before now fails.
10. Commit the file and the propagation edits as one logical change per concern with `git`, giving the reason and who decided it in the message. Record in the Outcome which documents were changed and which were left on purpose.

## Output
A revised rule file, with its list entry and neighbors consistent, and a commit.

## Success Criteria
- The change matches the stated reason and nothing more.
- Status and Confidence are a legal move in `.praxis/lifecycles/assertion-lifecycle.md`.
- `grep -rn` finds no reference to a name that no longer exists, and a search for the old wording finds only history.
- A walked case follows the new wording without a gap.
- The `modified` timestamp changed and `created` did not.

## Domain Alignment

None recorded yet; the domain lists are still being populated.

## Related Skills

- praxis-create-rule
- praxis-promote-assertion
- praxis-flow-learn
- praxis-flow-introspect
- praxis-flow-self-review

## Troubleshooting

### Issue: The reason is a single observation

Identifying:
The only support for the change is one Outcome or one remark.

Solution:
Record it as a note in the item and leave the content and confidence alone until it recurs independently, or the user directs the change.

### Issue: The change contradicts something the user stated directly

Identifying:
The rule came from a direct user statement and the evidence argues against it.

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
