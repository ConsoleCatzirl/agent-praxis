---
name: praxis-create-pattern
description: Create a new pattern in `.praxis/factory/patterns/` from its template, set its starting stage and confidence, align it with existing items, list it, and commit it. Use when a pattern is to be added to the Factory (`.praxis/factory/patterns/`).
confidence: Low
complexity: Qualitative
implements:
  - Create a Praxis Component
  - Track Confidence
---

# Skill: Praxis Create Pattern

Create a new pattern (an ordered list of factory products that compose to complete a kind of Task) in the Factory (`.praxis/factory/patterns/`).

## Origin
Initial Implementation

## Purpose
Add a pattern so that its file, its list entry, its alignment, and its confidence row agree, and so that it starts at the confidence and stage its origin supports.

## When to Use
When the user asks for a pattern, or a Flow stage (usually `praxis-flow-learn`, `praxis-flow-introspect` or `praxis-self-reflect`) proposes one and the user consents. Not for changing or removing an existing pattern; use `praxis-refine-pattern`.

## How it Works
The skill checks that the name is new, picks the starting stage and confidence from the evidenced lifecycle's entry paths, writes the item from `.praxis/templates/pattern-template.md`, aligns it with the domain items and factory products that already exist, and records it in the list and the confidence table. It then commits the result as one logical change.

## Requirements
- No consent is needed: a Pattern is a factory product, not a domain item. `praxis-flow-plan` may create one for a Plan.
- A name and content for the pattern.
- `.praxis/templates/pattern-template.md`, `.praxis/lifecycles/evidenced-lifecycle.md`, and `.praxis/lifecycles/confidence-lifecycle.md` exist.

## Inputs
A short name (the file name is `${item-name}.md`, lowercase and hyphenated), the content of the pattern, and its origin: a direct user statement, an indirect user statement, or the agent's own inference.

## Procedure
1. Read the following files if they are not already in context: `.praxis/factory/README.md`, `.praxis/factory/patterns/README.md`, `.praxis/factory/patterns.md`, `.praxis/templates/pattern-template.md`, `.praxis/lifecycles/evidenced-lifecycle.md`, and `.praxis/lifecycles/confidence-lifecycle.md`.
2. Check that the name is not already in `.praxis/factory/patterns.md`. If it is, stop and use `praxis-refine-pattern` instead of adding a second item.
3. Check the evidence: a Pattern needs a first occurrence or a Plan that uses it; several uses in one run count as one piece of evidence.
4. Choose the starting lifecycle stage and confidence (stages: Hypothesized, Evidenced, Established, Challenged, Debunked):
   - **Hypothesized at Low** when the agent originates the item from a first observation or inference.
   - **Hypothesized at Medium** when the user states it directly.
   - Never start above Hypothesized: Evidenced and Established need independent supporting observations.
5. Create `.praxis/factory/patterns/${item-name}.md` from the template, checking that its sections, stage, confidence and alignment are filled and consistent. Set both timestamps with `date -Iseconds` (ISO-8601 with seconds and timezone), the Status to the stage and the Confidence to the level from step 4. Fill every section, in the template's order and with the template's headings:
   - **Description**: a detailed description of what the pattern does.
   - **Origin**: what led to creating the pattern (the Task, Plan, or runs where the sequence occurred).
   - **Context**: where the pattern occurs and should be used.
   - **Procedure**: general prose: what is done, in general, in this kind of situation, and in what order. No paths and no product names; a Pattern has no complexity level.
   - **Implementing Skills**: at least one skill that implements the Pattern, with the situation each is for (Rule: Every Pattern MUST Be Implemented by at Least One Skill). Each skill must exist and must name this Pattern in the `implements:` of its frontmatter: add it there (`praxis-refine-skill`), or write a new skill first (`praxis-create-skill`). A deterministic sequence the skill runs is a habit (`praxis-create-habit`).
   - **Conditions for Revision**: what would put it into Challenged.
   - **Evidence Notes**: the independent runs that support it (several uses in one run count once), or a note that there are none yet.
   - **Confidence Alignment**: the patterns whose confidence correlates with this one.
   - **Domain Alignment**: Reinforcing / Ambiguous / Contradictory, each naming existing domain items.
6. Check every item named under Domain Alignment: it must exist in `.praxis/domains/` or `.praxis/factory/`. Read the neighbors in the other domains for tension, and list any tension as Ambiguous or Contradictory (or Unaligned) instead of leaving it out. Do not resolve a contradiction between items by choosing one: record it and propose a dialectical synthesis to the user.
7. Add the pattern to `.praxis/factory/patterns.md`, keeping the list in alphabetical order, linking to `.praxis/factory/patterns/${item-name}.md`, and replacing the template placeholder line if it is still there.
8. Add a row to `.praxis/tracking/confidence/patterns.csv` with the columns `confidence,lifecycle,details,name`, using the starting confidence and lifecycle stage from step 4 and the file name of the item.
9. Check the new pattern: its list entry, its template sections, its Status and Confidence and its alignment references all hold, every step of its Procedure names a product, and no check that passed before now fails.
10. Look for other documents that already state or contradict this pattern: `grep -rn -i` for its key words and their neighbors (inflections, synonyms, field names) across `.praxis/` (`flow.md`, `CLAUDE.md`, `README.md`, `glossary.md`, `lifecycles/`, `templates/`, `domains/`, `factory/`, `tracking/`; leave `state/` and git history alone, since they record what was true then). Where another document restates the same idea, say it once in the new pattern and have the other point to it; where one contradicts it, list the contradiction under Domain Alignment instead of editing the other document silently.
11. Commit the item, the list, the confidence table, and any pointer edits as one logical change with `git -C .praxis`, naming the pattern in the commit message.

## Output
A new pattern file in `.praxis/factory/patterns/`, its entry in `.praxis/factory/patterns.md`, its row in `.praxis/tracking/confidence/patterns.csv`, and a commit.

## Success Criteria
- The name appears exactly once in the list and as one file.
- No template section is empty or still holds its bracketed prompt.
- Every Domain Alignment reference resolves to an existing item.
- A search for the pattern's key words finds no document that states it differently without being listed as a contradiction.
- The starting stage and confidence are a legal entry path of `.praxis/lifecycles/evidenced-lifecycle.md`.
- Every step of the Procedure names one factory product that exists, and none is written as prose (read each step to check).
- Running the skill again for the same name changes nothing.

## Domain Alignment

None recorded yet; the lists are still being populated.

## Related Skills

- praxis-refine-pattern
- praxis-create-skill
- praxis-refine-skill
- praxis-flow-learn
- praxis-flow-introspect
- praxis-promote-evidenced

## Troubleshooting

### Issue: The name is already listed

Identifying:
`.praxis/factory/patterns.md` already links to an item with this name.

Solution:
Stop. Use `praxis-refine-pattern` to change the existing item, and tell the user.

### Issue: The new pattern contradicts an existing item

Identifying:
The existing item says the opposite, or would make this pattern impossible to follow.

Solution:
Create the pattern only if the user still wants it, list the contradiction under Domain Alignment, and propose a synthesis to the user. Do not abandon either item on the agent's authority.

### Issue: A template section does not fit

Identifying:
The content has nothing to put under a heading.

Solution:
Do not delete the heading. Write that nothing applies and why, or reconsider whether this is a pattern or belongs in another domain (see `.praxis/domains/README.md`).

### Issue: A step has no factory product

Identifying:
A step of the Procedure would be written as prose, or a step names no product.

Solution:
Do not write the prose into the Pattern. A mechanical step becomes a script (`praxis-create-script`); a step that needs judgement or instructions becomes a skill, new (`praxis-create-skill`) or an addition to an existing one (`praxis-refine-skill`). Then name that product in the step.

2026-11-24: used once (Write a Project Document From Read Sources). Steps 7 and 8 were done by hand, since the register option of add-item does not accept a Pattern; step 5 offers a JSON route of the same script that was not tried. Stays Low: one use.

## Notes

2026-11-24 (third run, Plan Write the 0-evidence mechanism skills for template/semantic): used for its intent to write three Patterns, text only, Hypothesized at Low, on a clone of a template branch in that branch's older Pattern template; the steps naming workspace scripts were done by hand. Stays Low.

2026-11-24 (fourth run, same Plan): used in this workspace; its step 5 named the script that adds items, whose registering option does not take a Pattern, so the list entry and row were written by hand (the script's JSON form was not tried). Stays Low.

2026-11-24 (fifth run, same Plan): used for 14 Patterns with the script that adds items, against a template branch; its row for the branch's table had the wrong columns and was rewritten, which a read of the branch's header before writing would have avoided. Stays Low.
