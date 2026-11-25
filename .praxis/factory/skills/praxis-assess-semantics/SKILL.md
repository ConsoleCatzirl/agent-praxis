---
name: praxis-assess-semantics
description: Assess the meaning of the Praxis records - each defined term has one meaning wherever it is used, each lifecycle makes sense for what it governs, and each complexity level is right. Use when the user asks for a semantic assessment, during introspection, or after terms or lifecycles were renamed or restructured.
confidence: Low
complexity: Qualitative
implements:
  - Assess Semantics
---

# Skill: Praxis Assess Semantics

Check that the words the Flow runs on mean one thing, that its state machines describe what the skills actually do, and that complexity levels say what they claim.

## Origin
The deep introspection of 2026-11-21 (the owner: "semantic assessment (consistent meanings, do the lifecycles make sense?, are complexity levels correct?)"). At its Plan the Phases were named three ways (`flow.md`: Anticipate, Act, Reflect; the glossary: Anticipate, Act, Reflect with Decompose and Plan inside Anticipate; `.praxis/CLAUDE.md`: Plan, Anticipate, Act, Reflect, Return), and the Patterns Add Domain Entry and Track Confidence were Structural although each names a skill.

## Purpose
Find terms with more than one meaning, lifecycles whose stages or paths do not match their use, and complexity levels that break their definitions, and propose one reading for each.

## When to Use
When the user asks for a semantic assessment; during `praxis-flow-introspect`; after a rename, a restructure, or a change to a lifecycle. Run it as a Pattern (Assess Semantics) inside a Plan, after Assess Structure (broken references make meanings hard to read).

## How it Works
Scripts find where terms are defined and used, which retired terms are still in use, and where complexity levels break the max rule; this skill compares the readings and judges whether lifecycles and levels make sense. Each step is labelled with its complexity level.

## Requirements
The structural assessment has run in the same Plan, or its findings are known.

## Inputs
- The same scope as `praxis-assess-structure`: `.praxis/` and the agent layer and documents of every project repository.
- The definition sites: `.praxis/glossary.md`, `.praxis/flow.md`, `.praxis/README.md`, the READMEs of `domains/`, `factory/`, `state/`, `tracking/`, `lifecycles/`, `templates/`, `.praxis/CLAUDE.md` and the `CLAUDE.md` of the workspace and of each project repository, and each lifecycle's Stages.

## Procedure
1. **Retired terms** (Regex). Run the habit `.praxis/factory/habits/run-the-semantic-checks/README.md` once; it runs the scripts of this step and of steps 3, 5 and 7. Here, `python3 -I .praxis/factory/scripts/termcheck/termcheck.py`: each use of a retired term (`termcheck/retired.txt`: the names and words the restructure of 2026-11-20 and later renames replaced) is listed with its file and line; quotations of the owner and history files are reported apart.
2. **Definition sites** (Regex). From the same run, take the list of glossary terms with every other file that defines them (a `**Term**:` list entry, a `## Term` heading, a `Term:` line in a README).
3. **Status words** (Mechanical). Run `python3 -I .praxis/factory/scripts/statuscheck/statuscheck.py`, then read the Requirements and Inputs sections of the Flow skills for status words (`Created`, `Proposed`, `Identified`, `Approved`, and the like) and check each against the lifecycle of the item it qualifies.
4. **One meaning per term** (Qualitative). For each term with more than one definition site, compare the readings. Record each pair that differs, with both readings, which file owns the term (`praxis-assess-structure` step 8), and the reading to keep. Look in particular at the Phases, the Bypass, Complexity, the stage names shared by several lifecycles (Approved, Rejected, Completed, Cleared), Domain Alignment's two vocabularies (Reinforcing/Ambiguous/Contradictory and Aligned/Unaligned), and the use of "entry", "item", and "product".
5. **Lifecycle graphs** (Structural). Run `python3 -I .praxis/factory/scripts/lifecyclecheck/lifecyclecheck.py` and keep its graph of each lifecycle.
6. **Lifecycles make sense** (Qualitative). For each lifecycle, check against what the skills actually do: every stage is entered by some skill and left by some skill; no two stages mean the same; a terminal stage is really terminal; a stage named in prose is in the Stages list; the lifecycle's entry and exit skills are the ones that set the status (`state.py set` calls in the skills); and the lifecycle fits what it governs (for example, whether a Bypassed Plan is ever Completed, and whether a Task needs a stage between Approved and Completed). Propose the smallest change that makes each one fit.
7. **Complexity: the max rule** (Structural). Run `python3 -I .praxis/factory/scripts/complexitycheck/complexitycheck.py`: each Pattern's Complexity equals the highest level of the products in its Procedure, each Plan's the highest of its Patterns, and the `complexity` columns of the tracking tables match the files.
8. **Complexity: the definitions** (Qualitative). For each product whose level the script cannot derive (a script's own label, a skill), compare it with the definitions in `.praxis/state/README.md` and `.praxis/factory/README.md`: a script that only uses globs and `sed` is Regex; glue of commands is Mechanical; one that needs data structures is Structural; a step that needs judgement is Qualitative and belongs in a skill. Record each level that does not fit, and each skill step that could move down a level (a candidate script).
9. **Triage and record** (Qualitative). As in `praxis-assess-structure` step 10: kind (term, status word, lifecycle, complexity), evidence, strength, and application (fixed now / needs consent / report only). A rename of a retired term to its current name is mechanical; choosing between two live readings is not.

10. If a script fails to run in any step, record the error, do its step by reading, and say the step was partial.

## Output
Semantic findings in the Plan's Outcome, each with kind, evidence, strength, and application, and for each term or lifecycle with conflicting readings the reading proposed.

## Success Criteria
- Every term with more than one definition site is compared, and each difference is recorded with both readings.
- Every lifecycle is judged against the skills that use it, with the result stated even when it is "makes sense".
- Every Pattern's complexity is checked against the max rule.
- No domain item is changed by the assessment; each proposed change is handed to `praxis-flow-learn`.

## Domain Alignment

Aligned
- Practice: Use Plain Language and Defined Terms
- Rule: Praxis Records MUST Conform to Their Templates and Lifecycles
- Rule: Every Prompt MUST Follow the Flow
- Value: Simplicity
- Practice: Right-Size a Task to the Least Powerful Machine That Does It

Unaligned
- none known

## Related Skills

- praxis-assess-structure
- praxis-assess-epistemics
- praxis-flow-introspect

## Troubleshooting

### Issue: Both readings are in use

Identifying:
Two files define a term differently and skills follow each.

Solution:
Do not pick one. Record both readings, which skills follow each, and a proposed reading for the owner; a change of meaning is never mechanical.

### Issue: A retired term is inside a quotation or a history record

Identifying:
`termcheck.py` reports the match as quoted, or the file is a record of what was true then (git history, an Evidence Note, an Origin).

Solution:
Leave it. Quotations and records keep their words.

## Notes

Lifecycle steps here judge meaning; their structural validity (reachability, path agreement) is `praxis-assess-structure` step 6.

2026-11-24 (fifth run, Plan Suggest naming schemes for the domain item types; Result Helpful): used for its reading of the domains, narrowed to the names of items and their purposes; none of its scripts was run. Stays Low.
