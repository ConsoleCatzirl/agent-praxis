---
name: praxis-create-intention
description: Create a new intention in `.praxis/domains/intentions/` from its template, set its starting stage and confidence, align it with existing items, list it, and commit it. Use when a intention is to be added to the `intentions` domain.
confidence: Low
complexity: Qualitative
---

# Skill: Praxis Create Intention

Create a new intention (a guiding purpose or indefinite goal) in the `intentions` domain.

## Origin
Praxis Template

## Purpose
Add a intention so that its file, its list entry, its alignment agree, and so that it starts at the confidence and stage its origin supports.

## When to Use
When the user asks for a intention, or a Flow stage (usually `praxis-flow-learn`, `praxis-flow-introspect` or `praxis-flow-self-review`) proposes one. Not for changing or removing an existing intention; use `praxis-refine-intention`.

## How it Works
The skill checks that the name is new, picks the starting stage and confidence from the assertion lifecycle's entry paths, writes the item from `.praxis/templates/intention-template.md`, aligns it with the items that already exist, and records it in the domain list. It then commits the result as one logical change.

## Requirements
- The owner's request for the intention, or the agent's case-by-case judgement that it may be added now (`CLAUDE.md`, "Domain and Tracking Changes").
- A name and content for the intention.
- `.praxis/templates/intention-template.md`, `.praxis/lifecycles/assertion-lifecycle.md`, and `.praxis/lifecycles/confidence-lifecycle.md` exist.

## Inputs
A short name (the file name is `${item-name}.md`, lowercase and hyphenated), the content of the intention, and its origin: a direct user statement, an indirect user statement, or the agent's own inference.

## Procedure
1. Read the following files if they are not already in context: `.praxis/domains/README.md`, `.praxis/domains/intentions/README.md`, `.praxis/domains/intentions.md`, `.praxis/templates/intention-template.md`, `.praxis/lifecycles/assertion-lifecycle.md`, and `.praxis/lifecycles/confidence-lifecycle.md`.
2. Check that the name is not already in `.praxis/domains/intentions.md`. If it is, stop and use `praxis-refine-intention` instead of adding a second item.
3. Judge, case by case, whether to add the intention now or to propose it to the owner first (`CLAUDE.md`, "Domain and Tracking Changes"); to propose it, stop here and name it in the `praxis-flow-learn` review.
4. Choose the starting lifecycle stage and confidence (stages: Proposed, Asserted, Questioned, Abandoned):
   - **Proposed at Low** when the agent originates the item (pattern recognition, an indirect user statement).
   - **Proposed at Medium** when the user states it with uncertainty, or the item has had a major revision.
   - **Asserted at High** only on a direct user statement. Complete is never a starting level.
5. Create `.praxis/domains/intentions/${item-name}.md` from the template, checking that its sections, stage, confidence and alignment are filled and consistent. Set both timestamps with `date -Iseconds` (ISO-8601 with seconds and timezone), the Status to the stage and the Confidence to the level from step 4. Fill every section, in the template's order and with the template's headings:
   - **Statement**: an infinitive or imperative phrase, or an indefinite qualitative goal.
   - **Basis**: the reasoning or evidence that supports the intention.
   - **Bounds**: the contexts or conditions in which the intention stops applying.
   - **Conditions for Revision**: what would put it into Questioned.
   - **Domain Alignment**: Reinforcing / Ambiguous / Contradictory, each naming existing domain items.
6. Check every item named under Domain Alignment: it must exist in `.praxis/domains/` or `.praxis/factory/`. Read the neighbors in the other domains for tension, and list any tension as Ambiguous or Contradictory (or Unaligned) instead of leaving it out. Do not resolve a contradiction between items by choosing one: record it and propose a dialectical synthesis to the user.
7. Add the intention to `.praxis/domains/intentions.md`, keeping the list in alphabetical order, linking to `.praxis/domains/intentions/${item-name}.md`, and replacing the template placeholder line if it is still there.
8. No confidence table covers this domain; the confidence lives only in the item's file.
9. Check the new intention: its list entry, template sections, Status, Confidence and alignment references all hold, and no check that passed before now fails.
10. Look for other documents that already state or contradict this intention: `grep -rn -i` for its key words and their neighbors (inflections, synonyms, field names) across `.praxis/` (`flow.md`, `CLAUDE.md`, `README.md`, `glossary.md`, `lifecycles/`, `templates/`, `domains/`, `factory/`, `tracking/`; leave `state/` and git history alone, since they record what was true then). Where another document restates the same idea, say it once in the new intention and have the other point to it; where one contradicts it, list the contradiction under Domain Alignment instead of editing the other document silently.
11. Commit the item, the list, and any pointer edits as one logical change with `git`, naming the intention in the commit message.

## Output
A new intention file in `.praxis/domains/intentions/`, its entry in `.praxis/domains/intentions.md`, and a commit.

## Success Criteria
- The name appears exactly once in the domain list and as one file.
- No template section is empty or still holds its bracketed prompt.
- Every Domain Alignment reference resolves to an existing item.
- A search for the intention's key words finds no document that states it differently without being listed as a contradiction.
- The starting stage and confidence are a legal entry path of `.praxis/lifecycles/assertion-lifecycle.md`.
- Running the skill again for the same name changes nothing.

## Domain Alignment

None recorded yet; the domain lists are still being populated.

## Related Skills

- praxis-refine-intention
- praxis-flow-learn
- praxis-flow-introspect
- praxis-promote-assertion

## Troubleshooting

### Issue: The name is already listed

Identifying:
`.praxis/domains/intentions.md` already links to an item with this name.

Solution:
Stop. Use `praxis-refine-intention` to change the existing item, and tell the user.

### Issue: The new intention contradicts an existing item

Identifying:
The existing item says the opposite, or would make this intention impossible to follow.

Solution:
Create the intention only if the user still wants it, list the contradiction under Domain Alignment, and propose a synthesis to the user. Do not abandon either item on the agent's authority.

### Issue: A template section does not fit

Identifying:
The content has nothing to put under a heading.

Solution:
Do not delete the heading. Write that nothing applies and why, or reconsider whether this is a intention or belongs in another domain (see `.praxis/domains/README.md`).
