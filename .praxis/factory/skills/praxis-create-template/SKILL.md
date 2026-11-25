---
name: praxis-create-template
description: Write a new template in `.praxis/templates/` for a kind of item, with its own frontmatter, whole-line placeholders, and the headings and fields its items need, and name the check scripts that must learn the item type. Use when a new kind of item is introduced.
confidence: Low
complexity: Qualitative
implements:
  - Create a Praxis Component
---

# Skill: praxis-create-template

## Origin
The owner, 2026-11-22: "create skills for creating lifecycles and templates", after the introspection template had to be written by hand (Plan Track Introspections as Items).

## Purpose
Give a new kind of item a template that the scripts can check and the skills can fill, so every item of the kind has the same headings and fields.

## When to Use
When a Plan adds a kind of item (a state item, a tracking record, a domain, a factory product type). To change an existing template, edit it with Pattern: Propagate a Rule Through Documents and check the items it governs.

## How it Works
The judgement is the fields and headings the items need and their order. `tmplcheck` checks items against templates; `state.py` and `tmplcheck` treat a whole-line `[ ... ]` as an unfilled placeholder, so the template's form decides what the scripts can see.

## Requirements
The kind of item, where its items live, and its lifecycle if it has stages (`praxis-create-lifecycle`).

## Inputs
The item kind's name (the heading word, as in `# Introspection: ...`), its directory, and its fields and sections.

## Procedure
1. Read `.praxis/templates/README.md` and two templates close to the new kind (for example `.praxis/templates/signal-template.md` and `.praxis/templates/analysis-template.md`). Check that no template in `.praxis/templates/` already covers the items; if one does, stop and change it instead.
2. Write `.praxis/templates/${kind}-template.md`:
   1. Its own frontmatter: `---`, `description: template for ...` naming the directory its items go in, `---`. If the items have frontmatter of their own, a second block follows with their fields (as `.praxis/templates/skill-template.md` does).
   2. The heading `# ${Kind}: [ Name ]`; the `created` and `modified` lines when the items keep timestamps; `Status: [ Lifecycle Stage ]` when they have a lifecycle; then each field as `Label: [ what goes here ]` and each section as `## Heading` followed by its placeholder.
   3. Every placeholder is a whole line or a whole list item in `[ ... ]` (or the whole value after a label), never part of a sentence, so `state.py` and `tmplcheck` recognize an unfilled field.
   4. Fields and headings in the order the items need them, with a placeholder that says what to write, not an example.
3. Name the template where its items are described: the README of the items' directory and the skill that creates the items.
4. Write a test item from the template by hand, in the scratchpad, filled in, and run `python3 -I .praxis/factory/scripts/tmplcheck/tmplcheck.py <its path>` on a copy placed where the items live; then delete the copy. If `tmplcheck` does not check the location, that is the first Task of step 5.
5. For a new item type, write a Task for each check script that must learn it (`python3 -I .praxis/factory/scripts/state/state.py new task "<name>"`, through `praxis-refine-script`), rather than editing them here: `tmplcheck.py` (`KIND_TEMPLATE` and the locations it checks), `layoutcheck.py` (the allowed paths), and `hygiene.py` (a list that must name exactly the items that exist, and each item's Status). For a state item, `state.py` (`KINDS`) too.
6. Stage the template and the README changes, run `python3 -I .praxis/factory/scripts/pre-commit-checks/pre-commit-checks.py`, and commit with `git -C .praxis` only when it passes.

## Output
A template in `.praxis/templates/`, named where its items are described; Tasks for the check scripts that must learn the item type.

## Success Criteria
- The template has its own frontmatter and whole-line placeholders, in the order the items need.
- A filled test item passes `tmplcheck` where the items live.
- Each check script that must learn a new item type has a Task.

## Domain Alignment

Aligned
- Rule: Praxis Records MUST Conform to Their Templates and Lifecycles
- Practice: Use Plain Language and Defined Terms
- Value: Reliability

Unaligned
- none known

## Related Skills

- praxis-create-lifecycle
- praxis-create-skill
- praxis-refine-script

## Troubleshooting

### Issue: An item cannot be told from a placeholder

Identifying:
`state.py` refuses a filled item as unwritten, or `tmplcheck` misses an unfilled one.

Solution:
Make every placeholder a whole line or list item in `[ ... ]`, and keep bracketed text in items mid-sentence (the check tells them apart by that).

## Notes

None.
