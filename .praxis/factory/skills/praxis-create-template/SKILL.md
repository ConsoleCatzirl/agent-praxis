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
Praxis Template

## Purpose
Give a new kind of item a template that the scripts can check and the skills can fill, so every item of the kind has the same headings and fields.

## When to Use
When a Plan adds a kind of item (a state item, a tracking record, a domain, a factory product type). To change an existing template, edit it, and check every item it governs.

## How it Works
The judgement is the fields and headings the items need and their order. Items are checked against templates by reading them; a whole-line `[ ... ]` marks an unfilled placeholder, so the template's form decides what can be seen as unfilled.

## Requirements
The kind of item, where its items live, and its lifecycle if it has stages (`praxis-create-lifecycle`).

## Inputs
The item kind's name (the heading word, as in `# Introspection: ...`), its directory, and its fields and sections.

## Procedure
1. Read `.praxis/templates/README.md` and two templates close to the new kind (for example `.praxis/templates/signal-template.md` and `.praxis/templates/analysis-template.md`). Check that no template in `.praxis/templates/` already covers the items; if one does, stop and change it instead.
2. Write `.praxis/templates/${kind}-template.md`:
   1. Its own frontmatter: `---`, `description: template for ...` naming the directory its items go in, `---`. If the items have frontmatter of their own, a second block follows with their fields (as `.praxis/templates/skill-template.md` does).
   2. The heading `# ${Kind}: [ Name ]`; the `created` and `modified` lines when the items keep timestamps; `Status: [ Lifecycle Stage ]` when they have a lifecycle; then each field as `Label: [ what goes here ]` and each section as `## Heading` followed by its placeholder.
   3. Every placeholder is a whole line or a whole list item in `[ ... ]` (or the whole value after a label), never part of a sentence, so an unfilled field is recognizable.
   4. Fields and headings in the order the items need them, with a placeholder that says what to write, not an example.
3. Name the template where its items are described: the README of the items' directory and the skill that creates the items.
4. Write a test item from the template by hand, in the scratchpad, filled in, and check it against the template on a copy placed where the items live (sections, headings and placeholders); then delete the copy. If nothing on the project checks that location, that is the first Task of step 5.
5. For a new item type, write a Task for each check or script on the project that must learn it, rather than editing them here: a check of items against templates (the kind and the locations it checks), a check of file locations (the allowed paths), and a check of lists and statuses (a list that must name exactly the items that exist, and each item's Status). For a state item, the script that handles state items too. A branch with no scripts has nothing to do in this step.
6. Stage the template and the README changes, check that the template and the README read correctly, and commit with `git -C .praxis` only when it passes.

## Output
A template in `.praxis/templates/`, named where its items are described; Tasks for the check scripts that must learn the item type.

## Success Criteria
- The template has its own frontmatter and whole-line placeholders, in the order the items need.
- A filled test item matches the template, section by section, where the items live.
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
A filled item is read as unwritten, or an unfilled one is missed.

Solution:
Make every placeholder a whole line or list item in `[ ... ]`, and keep bracketed text in items mid-sentence (the check tells them apart by that).

## Notes

None.
