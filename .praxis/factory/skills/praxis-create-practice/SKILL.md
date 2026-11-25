---
name: praxis-create-practice
description: Create a new practice in `.praxis/domains/practices/` from its template, set its starting stage and confidence, align it with existing items, list it, and commit it. Use when a practice is to be added to the `practices` domain.
confidence: Low
complexity: Qualitative
---

# Skill: Praxis Create Practice

Create a new practice (an imperative way of doing things (a modus operandi)) in the `practices` domain.

## Origin
Taken from the workspace's skill of the same name, without its run evidence; no recorded use on this branch.

## Purpose
Add a practice so that its file, its list entry, its alignment agree, and so that it starts at the confidence and stage its origin supports.

## When to Use
When the user asks for a practice, or a Flow stage (usually `praxis-flow-learn`, `praxis-flow-introspect` or `praxis-self-reflect`) proposes one. Not for changing or removing an existing practice; use `praxis-refine-practice`.

## How it Works
The skill checks that the name is new, picks the starting stage and confidence from the assertion lifecycle's entry paths, writes the item from `.praxis/templates/practice-template.md`, aligns it with the items that already exist, and records it in the domain list. It then commits the result as one logical change.

## Requirements
- The owner's request for the practice, or the agent's case-by-case judgement that it may be added now (`CLAUDE.md`, "Domain and Tracking Changes").
- A name and content for the practice.
- `.praxis/templates/practice-template.md`, `.praxis/lifecycles/assertion-lifecycle.md`, and `.praxis/lifecycles/confidence-lifecycle.md` exist.

## Inputs
A short name (the file name is `${item-name}.md`, lowercase and hyphenated), the content of the practice, and its origin: a direct user statement, an indirect user statement, or the agent's own inference.

## Procedure
1. Read the following files if they are not already in context: `.praxis/domains/README.md`, `.praxis/domains/practices/README.md`, `.praxis/domains/practices.md`, `.praxis/templates/practice-template.md`, `.praxis/lifecycles/assertion-lifecycle.md`, and `.praxis/lifecycles/confidence-lifecycle.md`.
2. Check that the name is not already in `.praxis/domains/practices.md`. If it is, stop and use `praxis-refine-practice` instead of adding a second item.
3. Judge, case by case, whether to add the practice now or to propose it to the owner first (`CLAUDE.md`, "Domain and Tracking Changes"); to propose it, stop here and name it in the `praxis-flow-learn` review.
4. Choose the starting lifecycle stage and confidence (stages: Proposed, Asserted, Questioned, Abandoned):
   - **Proposed at Low** when the agent originates the item (pattern recognition, an indirect user statement).
   - **Proposed at Medium** when the user states it with uncertainty, or the item has had a major revision.
   - **Asserted at High** only on a direct user statement. Complete is never a starting level.
5. Create `.praxis/domains/practices/${item-name}.md` from the template, checking that its sections, stage, confidence and alignment are filled and consistent. Set both timestamps with `date -Iseconds` (ISO-8601 with seconds and timezone), the Status to the stage and the Confidence to the level from step 4. Fill every section, in the template's order and with the template's headings:
   - **Statement**: a clear, actionable imperative.
   - **Basis**: the evidence or reasoning that supports the practice.
   - **Context**: where the practice does and does not apply.
   - **Conditions for Revision**: what would put it into Questioned.
   - **Domain Alignment**: Reinforcing / Ambiguous / Contradictory, each naming existing domain items.
6. Check every item named under Domain Alignment: it must exist in `.praxis/domains/` or `.praxis/factory/`. Read the neighbors in the other domains for tension, and list any tension as Ambiguous or Contradictory (or Unaligned) instead of leaving it out. Do not resolve a contradiction between items by choosing one: record it and propose a dialectical synthesis to the user.
7. Add the practice to `.praxis/domains/practices.md`, keeping the list in alphabetical order, linking to `.praxis/domains/practices/${item-name}.md`, and replacing the template placeholder line if it is still there.
8. No confidence table covers this domain; the confidence lives only in the item's file.
9. Check the new practice: its list entry, template sections, Status, Confidence and alignment references all hold, and no check that passed before now fails.
10. Look for other documents that already state or contradict this practice: `grep -rn -i` for its key words and their neighbors (inflections, synonyms, field names) across `.praxis/` (`flow.md`, `CLAUDE.md`, `README.md`, `glossary.md`, `lifecycles/`, `templates/`, `domains/`, `factory/`, `tracking/`; leave `state/` and git history alone, since they record what was true then). Where another document restates the same idea, say it once in the new practice and have the other point to it; where one contradicts it, list the contradiction under Domain Alignment instead of editing the other document silently.
11. Commit the item, the list, and any pointer edits as one logical change with `git`, naming the practice in the commit message.

## Output
A new practice file in `.praxis/domains/practices/`, its entry in `.praxis/domains/practices.md`, and a commit.

## Success Criteria
- The name appears exactly once in the domain list and as one file.
- No template section is empty or still holds its bracketed prompt.
- Every Domain Alignment reference resolves to an existing item.
- A search for the practice's key words finds no document that states it differently without being listed as a contradiction.
- The starting stage and confidence are a legal entry path of `.praxis/lifecycles/assertion-lifecycle.md`.
- Running the skill again for the same name changes nothing.

## Domain Alignment

None recorded yet; the domain lists are still being populated.

## Related Skills

- praxis-refine-practice
- praxis-flow-learn
- praxis-flow-introspect
- praxis-promote-assertion

## Troubleshooting

### Issue: The name is already listed

Identifying:
`.praxis/domains/practices.md` already links to an item with this name.

Solution:
Stop. Use `praxis-refine-practice` to change the existing item, and tell the user.

### Issue: The new practice contradicts an existing item

Identifying:
The existing item says the opposite, or would make this practice impossible to follow.

Solution:
Create the practice only if the user still wants it, list the contradiction under Domain Alignment, and propose a synthesis to the user. Do not abandon either item on the agent's authority.

### Issue: A template section does not fit

Identifying:
The content has nothing to put under a heading.

Solution:
Do not delete the heading. Write that nothing applies and why, or reconsider whether this is a practice or belongs in another domain (see `.praxis/domains/README.md`).
