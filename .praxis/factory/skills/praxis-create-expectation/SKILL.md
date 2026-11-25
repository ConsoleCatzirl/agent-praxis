---
name: praxis-create-expectation
description: Create a new expectation in `.praxis/domains/expectations/` from its template, set its starting stage and confidence, align it with existing items, list it, and commit it. Use when a expectation is to be added to the `expectations` domain.
confidence: Low
complexity: Qualitative
---

# Skill: Praxis Create Expectation

Create a new expectation (a generalized, reasonable effect or result to anticipate) in the `expectations` domain.

## Origin
Taken from the workspace's skill of the same name, without its run evidence; no recorded use on this branch.

## Purpose
Add a expectation so that its file, its list entry, its alignment, and its confidence row agree, and so that it starts at the confidence and stage its origin supports.

## When to Use
When the user asks for a expectation, or a Flow stage (usually `praxis-flow-learn`, `praxis-flow-introspect` or `praxis-flow-self-review`) proposes one. Not for changing or removing an existing expectation; use `praxis-refine-expectation`.

## How it Works
The skill checks that the name is new, picks the starting stage and confidence from the evidenced lifecycle's entry paths, writes the item from `.praxis/templates/expectation-template.md`, aligns it with the items that already exist, and records it in the domain list and the confidence table. It then commits the result as one logical change.

## Requirements
- The owner's request for the expectation, or the agent's case-by-case judgement that it may be added now (`CLAUDE.md`, "Domain and Tracking Changes").
- A name and content for the expectation.
- `.praxis/templates/expectation-template.md`, `.praxis/lifecycles/evidenced-lifecycle.md`, and `.praxis/lifecycles/confidence-lifecycle.md` exist.

## Inputs
A short name (the file name is `${item-name}.md`, lowercase and hyphenated), the content of the expectation, and its origin: a direct user statement, an indirect user statement, or the agent's own inference.

## Procedure
1. Read the following files if they are not already in context: `.praxis/domains/README.md`, `.praxis/domains/expectations/README.md`, `.praxis/domains/expectations.md`, `.praxis/templates/expectation-template.md`, `.praxis/lifecycles/evidenced-lifecycle.md`, and `.praxis/lifecycles/confidence-lifecycle.md`.
2. Check that the name is not already in `.praxis/domains/expectations.md`. If it is, stop and use `praxis-refine-expectation` instead of adding a second item.
3. Judge, case by case, whether to add the expectation now or to propose it to the owner first (`CLAUDE.md`, "Domain and Tracking Changes"); to propose it, stop here and name it in the `praxis-flow-learn` review.
4. Choose the starting lifecycle stage and confidence (stages: Hypothesized, Evidenced, Established, Challenged, Debunked):
   - **Hypothesized at Low** when the agent originates the item from a first observation or inference.
   - **Hypothesized at Medium** when the user states it directly.
   - Never start above Hypothesized: Evidenced and Established need independent supporting observations.
5. Create `.praxis/domains/expectations/${item-name}.md` from the template, checking that its sections, stage, confidence and alignment are filled and consistent. Set both timestamps with `date -Iseconds` (ISO-8601 with seconds and timezone), the Status to the stage and the Confidence to the level from step 4. Fill every section, in the template's order and with the template's headings:
   - **Statement**: one sentence of the form `P if/when Q`.
   - **Basis**: the reasoning or rationale behind the expectation.
   - **Bounds**: the contexts or conditions in which the expectation stops applying.
   - **Conditions for Revision**: what would put it into Challenged.
   - **Domain Alignment**: Reinforcing / Ambiguous / Contradictory, each naming existing domain items.
   - **Evidence Notes**: the Predictions and Outcomes that support or contradict it, or a note that there are none yet.
6. Check every item named under Domain Alignment: it must exist in `.praxis/domains/` or `.praxis/factory/`. Read the neighbors in the other domains for tension, and list any tension as Ambiguous or Contradictory (or Unaligned) instead of leaving it out. Do not resolve a contradiction between items by choosing one: record it and propose a dialectical synthesis to the user.
7. Add the expectation to `.praxis/domains/expectations.md`, keeping the list in alphabetical order, linking to `.praxis/domains/expectations/${item-name}.md`, and replacing the template placeholder line if it is still there.
8. Add a row to `.praxis/tracking/confidence/expectations.csv` with the columns `confidence,lifecycle,details,name`, using the starting confidence and lifecycle stage from step 4 and the file name of the item.
9. Check the new expectation: its list entry, template sections, Status, Confidence and alignment references all hold, and no check that passed before now fails.
10. Look for other documents that already state or contradict this expectation: `grep -rn -i` for its key words and their neighbors (inflections, synonyms, field names) across `.praxis/` (`flow.md`, `CLAUDE.md`, `README.md`, `glossary.md`, `lifecycles/`, `templates/`, `domains/`, `factory/`, `tracking/`; leave `state/` and git history alone, since they record what was true then). Where another document restates the same idea, say it once in the new expectation and have the other point to it; where one contradicts it, list the contradiction under Domain Alignment instead of editing the other document silently.
11. Commit the item, the list, the confidence table, and any pointer edits as one logical change with `git`, naming the expectation in the commit message.

## Output
A new expectation file in `.praxis/domains/expectations/`, its entry in `.praxis/domains/expectations.md`, its row in `.praxis/tracking/confidence/expectations.csv`, and a commit.

## Success Criteria
- The name appears exactly once in the domain list and as one file.
- No template section is empty or still holds its bracketed prompt.
- Every Domain Alignment reference resolves to an existing item.
- A search for the expectation's key words finds no document that states it differently without being listed as a contradiction.
- The starting stage and confidence are a legal entry path of `.praxis/lifecycles/evidenced-lifecycle.md`.
- Running the skill again for the same name changes nothing.

## Domain Alignment

None recorded yet; the domain lists are still being populated.

## Related Skills

- praxis-refine-expectation
- praxis-flow-learn
- praxis-flow-introspect
- praxis-promote-evidenced

## Troubleshooting

### Issue: The name is already listed

Identifying:
`.praxis/domains/expectations.md` already links to an item with this name.

Solution:
Stop. Use `praxis-refine-expectation` to change the existing item, and tell the user.

### Issue: The new expectation contradicts an existing item

Identifying:
The existing item says the opposite, or would make this expectation impossible to follow.

Solution:
Create the expectation only if the user still wants it, list the contradiction under Domain Alignment, and propose a synthesis to the user. Do not abandon either item on the agent's authority.

### Issue: A template section does not fit

Identifying:
The content has nothing to put under a heading.

Solution:
Do not delete the heading. Write that nothing applies and why, or reconsider whether this is a expectation or belongs in another domain (see `.praxis/domains/README.md`).
