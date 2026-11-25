---
name: praxis-assess-epistemics
description: Assess the epistemic commitments of the domains and the factory - each domain item is in the domain its content fits, ambiguities and contradictions are found (within and between domains, and between the domain items and the commitments of the project repositories), and each factory product aligns with the domain items it claims. Use when the user asks for an epistemic assessment, during introspection, or after many domain changes.
confidence: Low
complexity: Qualitative
implements:
  - Assess Epistemics
---

# Skill: Praxis Assess Epistemics

Check what the agent holds to be true, good, and required: that each commitment is filed as the kind of commitment it is, that the commitments agree with each other and with the commitments of the project repositories they serve, and that the factory actually carries them out.

## Origin
The deep introspection of 2026-11-21 (the owner: "epistemic assessment (are domain items in optimal domains?, ambiguity or contradictions? do factory products align with domain items?)").

## Purpose
Propose better domains for misfiled items, state each ambiguity and contradiction (a contradiction between Asserted items as thesis, antithesis, and synthesis), and list where the factory and the domains disagree.

## When to Use
When the user asks for an epistemic assessment; during `praxis-flow-introspect`; after a carry-over or many domain changes. Run it as a Pattern (Assess Epistemics) inside a Plan, after Assess Structure and Assess Semantics (misread terms make false contradictions).

## How it Works
Scripts produce candidate lists (items whose wording does not fit their domain's markers; the alignment graph with its asymmetries and unclaimed Asserted items); this skill reads the candidates and the sources and judges. Nearly every step here is Qualitative; the scripts only narrow what to read.

## Requirements
The structural and semantic assessments have run in the same Plan, or their findings are known. Domain items are read, never changed: a change is handed to `praxis-flow-learn` as a proposal.

## Inputs
- `.praxis/domains/README.md` (the domain definitions), each domain's README, list, and items.
- `.praxis/factory/` products and Patterns, with their Domain Alignment sections.
- The commitments of every project repository of the workspace (a directory with its own `.git`, other than `.praxis/`): its `CLAUDE.md` (invariants, working rules), and its design and process documents.
- `.praxis/tracking/confidence/*.csv` for confidence against status.

## Procedure
1. **Domain-fit markers** (Regex). Run the habit `.praxis/factory/habits/run-the-epistemic-checks/README.md` once; it runs this step's script and step 3's. Here, `python3 -I .praxis/factory/scripts/domainfit/domainfit.py`: rules without MUST or SHOULD, beliefs and expectations that prescribe (MUST, SHOULD, an imperative), practices whose name does not start with a verb, values that are not qualities, environment items with no date or no way to check them, and items whose Description restates another domain's item.
2. **Domain fit** (Qualitative). Read each flagged item and the definitions in `.praxis/domains/README.md`. Decide whether the item is in the domain its content fits: a falsifiable statement is a belief; a generalized effect is an expectation; a current condition is environment; a purpose is an intention; a preference is an opinion; a way of doing things is a practice; a rationale is a principle; a requirement is a rule; an ideal quality is a value. For each misfit, propose the domain and the restated item, and say what it would gain or lose (an Asserted practice moved to opinions would stop being enforced).
3. **Alignment graph** (Structural). Run `python3 -I .praxis/factory/scripts/aligncheck/aligncheck.py`: asymmetric pairs, references to items in Questioned, Abandoned, Challenged, or Debunked, items no other item or product names, Asserted items no factory product names, and every Ambiguous and Contradictory pair.
4. **Ambiguity and contradiction in the domains** (Qualitative). Read each Ambiguous and Contradictory pair, and each pair of items whose names or Descriptions overlap (the script lists overlaps by shared words). Record each ambiguity (one item can be read two ways, or two items cover the same ground with different words) and each contradiction (following one breaks the other). Check confidence against status: an Asserted item below High, a Hypothesized item above Medium, a tracking row that disagrees with its item. State a contradiction between Asserted items as thesis, antithesis, and a proposed synthesis that keeps what each protects (`.praxis/glossary.md`, Dialectical Synthesis).
5. **Project commitments** (Qualitative). Read the documents of every project repository of the workspace (a directory with its own `.git`, other than `.praxis/`) and list its commitments (a statement the project requires or holds: an invariant, a branching or commit rule, a decided design question, a "never"). For each domain item that bears on a project's work (a Rule or Practice about commits, branches, directories, documents or scope), find the commitments it touches, and record: a domain item that contradicts a commitment; a commitment the domains rely on that no item holds; a domain item worded more strongly or weakly than the commitment; and a commitment stated in two incompatible ways in different documents (a specification leads over any `CLAUDE.md` summary of it). Quote the source line. A conflict between a project's own documents is reported, not resolved here.
6. **Factory against domains** (Qualitative). For each factory product and Pattern, read its Domain Alignment against what its Procedure or code does: does it carry out the items it names, does it work against an item it does not name, and does it name an item that does not apply? For each Asserted item that no product names (step 3), say whether some product carries it out anyway (then the alignment is missing) or none does (then it is enforced by the agent alone).
7. **Triage and record** (Qualitative). For every finding record: kind (domain fit, ambiguity, contradiction, confidence-status, project commitment, factory alignment), evidence (file and line), strength, and application. Domain changes always need consent; a missing alignment line in a factory product is mechanical when the product plainly carries the item out (its Procedure names the item's mechanism).

8. If a script fails to run in any step, record the error, read the domain lists in full instead, and say the step was partial.

## Output
Epistemic findings in the Plan's Outcome; each contradiction between Asserted items with thesis, antithesis, and synthesis; each domain move with the restated item; all handed to `praxis-flow-learn` for consent.

## Success Criteria
- Every flagged item was read and judged, and every domain has its result stated (findings or "none").
- Every Asserted contradiction has a proposed synthesis or is reported as having none.
- Every domain item that bears on a project repository is traced to the commitment it touches, or recorded as having none.
- No domain item was changed.

## Domain Alignment

Aligned
- Principle: Synthesis of Contradictions
- Belief: Contradictions Are Informative
- Value: Reliable Self-Knowledge
- Practice: Ground Each Premise in a Read or a Trial, Not Memory

Unaligned
- none known

## Related Skills

- praxis-assess-structure
- praxis-assess-semantics
- praxis-flow-introspect
- praxis-flow-learn
- praxis-promote-assertion
- praxis-promote-evidenced

## Troubleshooting

### Issue: A misfit item was created from the owner's words

Identifying:
The item's Origin quotes the owner.

Solution:
Do not propose moving it on the agent's authority alone. Present it as a contradiction between the item's wording and its domain's definition, and let the owner choose.

### Issue: A project document is empty or a stub

Identifying:
A document named in Inputs is empty, or a section says it is to be written.

Solution:
Record the commitment as not yet stated; do not infer what the document will say.

## Notes

The project repositories' documents are the owner's statements of what the projects require; whether they are right is not this skill's question. The question is whether the domain items agree with them, and with each other.
