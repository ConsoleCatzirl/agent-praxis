---
name: praxis-create-belief
description: Create a new belief in `.praxis/domains/beliefs/` from its template, set its starting stage and confidence, align it with existing items, list it, and commit it. Use when a belief is to be added to the `beliefs` domain.
confidence: Low
complexity: Qualitative
---

# Skill: Praxis Create Belief

Create a new belief (a falsifiable statement developed through evidence and inference) in the `beliefs` domain.

## Origin
Taken from the workspace's skill of the same name, without its run evidence; no recorded use on this branch.

## Purpose
Add a belief so that its file, its list entry, its alignment, and its confidence row agree, and so that it starts at the confidence and stage its origin supports.

## When to Use
When the user asks for a belief, or a Flow stage (usually `praxis-flow-learn`, `praxis-flow-introspect` or `praxis-self-reflect`) proposes one. Not for changing or removing an existing belief; use `praxis-refine-belief`.

## How it Works
The skill checks that the name is new, picks the starting stage and confidence from the evidenced lifecycle's entry paths, writes the item from `.praxis/templates/belief-template.md`, aligns it with the items that already exist, and records it in the domain list and the confidence table. It then commits the result as one logical change.

## Requirements
- The owner's request for the belief, or the agent's case-by-case judgement that it may be added now (`CLAUDE.md`, "Domain and Tracking Changes").
- A name and content for the belief.
- `.praxis/templates/belief-template.md`, `.praxis/lifecycles/evidenced-lifecycle.md`, and `.praxis/lifecycles/confidence-lifecycle.md` exist.

## Inputs
A short name (the file name is `${item-name}.md`, lowercase and hyphenated), the content of the belief, and its origin: a direct user statement, an indirect user statement, or the agent's own inference.

## Procedure
1. Read the following files if they are not already in context: `.praxis/domains/README.md`, `.praxis/domains/beliefs/README.md`, `.praxis/domains/beliefs.md`, `.praxis/templates/belief-template.md`, `.praxis/lifecycles/evidenced-lifecycle.md`, and `.praxis/lifecycles/confidence-lifecycle.md`.
2. Check that the name is not already in `.praxis/domains/beliefs.md`. If it is, stop and use `praxis-refine-belief` instead of adding a second item.
3. Judge, case by case, whether to add the belief now or to propose it to the owner first (`CLAUDE.md`, "Domain and Tracking Changes"); to propose it, stop here and name it in the `praxis-flow-learn` review.
4. Choose the starting lifecycle stage and confidence (stages: Hypothesized, Evidenced, Established, Challenged, Debunked):
   - **Hypothesized at Low** when the agent originates the item from a first observation or inference.
   - **Hypothesized at Medium** when the user states it directly.
   - Never start above Hypothesized: Evidenced and Established need independent supporting observations.
5. Create `.praxis/domains/beliefs/${item-name}.md` from the template (or run the `add-item` script of the workspace (not on this branch: do the step by hand), which does this step and steps 7 and 8 after checking sections, stage, confidence, and alignment; see its docstring for the JSON). Set both timestamps with `date -Iseconds` (ISO-8601 with seconds and timezone), the Status to the stage and the Confidence to the level from step 4. Fill every section, in the template's order and with the template's headings:
   - **Statement**: a clear, falsifiable statement of what is believed to be true; if no observation could contradict it, rewrite it or make it an Opinion or Principle.
   - **Basis**: the evidence or reasoning that supports it.
   - **Bounds**: the contexts or conditions in which the belief stops applying.
   - **Conditions for Revision**: what evidence would put it into Challenged.
   - **Domain Alignment**: Reinforcing / Ambiguous / Contradictory, each naming existing domain items.
   - **Evidence Notes**: the supporting and contradicting evidence, or an explicit note that there is none yet.
6. Check every item named under Domain Alignment: it must exist in `.praxis/domains/` or `.praxis/factory/`. Read the neighbors in the other domains for tension, and list any tension as Ambiguous or Contradictory (or Unaligned) instead of leaving it out. Do not resolve a contradiction between items by choosing one: record it and propose a dialectical synthesis to the user.
7. Add the belief to `.praxis/domains/beliefs.md`, keeping the list in alphabetical order, linking to `.praxis/domains/beliefs/${item-name}.md`, and replacing the template placeholder line if it is still there.
8. Add a row to `.praxis/tracking/confidence/beliefs.csv` with the columns `confidence,lifecycle,details,name`, using the starting confidence and lifecycle stage from step 4 and the file name of the item.
9. Run the `checks` script of the workspace (not on this branch: do the step by hand): it must exit 0, with no check above its baseline (hygiene and tmplcheck, among its checks, cover the new belief).
10. Look for other documents that already state or contradict this belief: `grep -rn -i` for its key words and their neighbors (inflections, synonyms, field names) across `.praxis/` (`flow.md`, `CLAUDE.md`, `README.md`, `glossary.md`, `lifecycles/`, `templates/`, `domains/`, `factory/`, `tracking/`; leave `state/` and git history alone, since they record what was true then). Where another document restates the same idea, say it once in the new belief and have the other point to it; where one contradicts it, list the contradiction under Domain Alignment instead of editing the other document silently.
11. Commit the item, the list, the confidence table, and any pointer edits as one logical change with `git`, naming the belief in the commit message.

## Output
A new belief file in `.praxis/domains/beliefs/`, its entry in `.praxis/domains/beliefs.md`, its row in `.praxis/tracking/confidence/beliefs.csv`, and a commit.

## Success Criteria
- The name appears exactly once in the domain list and as one file.
- No template section is empty or still holds its bracketed prompt.
- Every Domain Alignment reference resolves to an existing item.
- A search for the belief's key words finds no document that states it differently without being listed as a contradiction.
- The starting stage and confidence are a legal entry path of `.praxis/lifecycles/evidenced-lifecycle.md`.
- Running the skill again for the same name changes nothing.

## Domain Alignment

None recorded yet; the domain lists are still being populated.

## Related Skills

- praxis-refine-belief
- praxis-flow-learn
- praxis-flow-introspect
- praxis-promote-evidenced

## Troubleshooting

### Issue: The name is already listed

Identifying:
`.praxis/domains/beliefs.md` already links to an item with this name.

Solution:
Stop. Use `praxis-refine-belief` to change the existing item, and tell the user.

### Issue: The new belief contradicts an existing item

Identifying:
The existing item says the opposite, or would make this belief impossible to follow.

Solution:
Create the belief only if the user still wants it, list the contradiction under Domain Alignment, and propose a synthesis to the user. Do not abandon either item on the agent's authority.

### Issue: A template section does not fit

Identifying:
The content has nothing to put under a heading.

Solution:
Do not delete the heading. Write that nothing applies and why, or reconsider whether this is a belief or belongs in another domain (see `.praxis/domains/README.md`).
