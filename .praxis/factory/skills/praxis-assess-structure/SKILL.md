---
name: praxis-assess-structure
description: Assess the structure of `.praxis/` and the agent layer and documents of every project repository - links and paths resolve, files follow their templates, lifecycles are valid state machines, files are where their READMEs put them, and content is in the file that owns it. Use when the user asks for a structural assessment, during introspection, or after a restructure.
confidence: Low
complexity: Qualitative
---

# Skill: Praxis Assess Structure

Check that the records the Flow reads and writes are well formed and in their places, so that Rule: Praxis Records MUST Conform to Their Templates and Lifecycles holds in fact and not only in the checks that happen to exist.

## Origin
Praxis Template

## Purpose
Find every structural defect in scope, fix the mechanical ones when the Plan allows it, and hand the rest to `praxis-flow-learn` with evidence.

## When to Use
When the user asks for a structural assessment; as part of `praxis-flow-introspect` (its step 8, Cohesion and conformance, is the narrow form of this skill); after a restructure, a rename, or a carry-over. Run it inside a Plan.

## How it Works
The sweeping checks are scripts; this skill runs them, reads what they report, and does the parts that need judgement: whether a reported defect is real, what its correct form is, and whether content belongs in another file. Each step is labelled with its complexity level (`.praxis/state/README.md`), so steps below Qualitative can move to scripts.

## Requirements
`.praxis/` is a git repository (Environment: Praxis Is a Nested Git Repository).

## Inputs
- Scope: `.praxis/` (without `.git/`; `state/` only for the live run's conformance) and the agent layer and documents of every project repository (a directory of the workspace with its own `.git`, other than `.praxis/`): the workspace's `CLAUDE.md`, `.claude/` (skill and agent links, settings), `.gitignore`, the auto-memory directory (`~/.claude/projects/<project>/memory/`), and, for each project repository, its `CLAUDE.md`, its `.claude/` if it has one, and the Markdown links of its documents.
- Optionally, a narrower scope or a list of files from the user or the Plan.

## Procedure
1. **Scope** (Mechanical). List the files in scope; state the count per area. If the Plan narrows the scope, say what was left out.
2. **Cohesion** (Structural). Check by reading that lists match their directories, statuses and confidences are valid, alignment references resolve, tracking rows match items, skill names equal their directories.
3. **Links** (Mechanical). Check every link in every Markdown file in scope: its target exists. A link whose target starts with `.praxis/` is the list-file convention and resolves from the workspace root.
4. **References** (Mechanical). Check that backticked paths and `praxis-*` skill names name files and skills that exist, and list the skills that other skills call that are not linked.
5. **Templates** (Structural). For each kind of file that has a template (domain items, Patterns, Signals, skills, product READMEs, state items, lifecycles, domain lists and domain READMEs), read two files of that kind against the template and record what differs: missing or extra sections, wrong headings, empty placeholders.
6. **Lifecycles** (Structural). Check that each Stages list equals its Stage Flow, that status phrases in skills name real stages, that every stage is reachable from New and able to reach Cleared, that each stage's Exit Paths give the same targets as the Stage Flow, and that skills named in Entry and Exit Paths exist.
7. **Locations** (Mechanical). Check that each file sits where a README says files of its kind go (a skill directory holds `SKILL.md` and `references/README.md`; a product directory holds `README.md`), no file is empty, nothing generated (`__pycache__`) is tracked, and the workspace `.gitignore` ignores `.praxis/` and `.claude/settings.local.json` and does not ignore the agent's installed skills.
8. **Ownership of content** (Qualitative). For the files the checks flagged, and for each definition that appears in more than one file (the glossary, READMEs, lifecycles, `flow.md`, and the `CLAUDE.md` of the workspace and of each project repository), decide which file owns it: the glossary defines terms, a lifecycle defines its stages, a README defines its directory's layout, a skill defines its procedure, a template defines a file's shape, `CLAUDE.md` points to the others, and a project's `CLAUDE.md` summarizes what the project's specification decides. Record each restatement that differs from its owner, and each piece of content that sits in a file that does not own it, with the file it belongs in.
9. **Judge each finding** (Qualitative). Confirm each script finding by reading the line; drop false positives and record them as a limit of the script. Give each finding its correct form, if one is determined by a file that exists (then it is mechanical), or the choices (then it needs the owner).
10. **Triage and record** (Qualitative). For every finding record: kind (link, reference, template, lifecycle, location, ownership), evidence (file and line, or commit), strength (Weak, Moderate, Strong), and application: **fixed now** (mechanical, outside `.praxis/domains/`, and the Plan allows fixes), **needs consent** (a domain item, a convention, a choice between readings, content moved between files), or **report only**. Write them into the Plan's Outcome; re-run steps 2-7 after any fixes and record the counts before and after.

11. If a script fails to run in any step, record the error, do its step by reading a sample of the files, and say the step was partial.

## Output
A list of structural findings in the Plan's Outcome, each with kind, evidence, strength and application; the scripts' counts before and after fixes; the fixes made, each as its own commit.

## Success Criteria
- Every step ran, or the Outcome says why it was partial.
- Every finding cites a file and line or a commit; a kind with no findings is stated as "none".
- No file in `.praxis/domains/` was changed by the assessment; each proposed change is handed to `praxis-flow-learn`.
- The scripts' counts after the fixes are recorded and each remaining finding is classed as a proposal for `praxis-flow-learn` or report only.

## Domain Alignment

Aligned
- Rule: Praxis Records MUST Conform to Their Templates and Lifecycles
- Practice: Right-Size a Task to the Least Powerful Machine That Does It
- Practice: Verify Generated Output Before Committing
- Practice: Cross-Check Paired Documents After Substantial or Accumulated Changes

Unaligned
- none known

## Related Skills

- praxis-assess-semantics
- praxis-assess-epistemics
- praxis-flow-introspect
- praxis-flow-verify-state
- praxis-refine-script

## Troubleshooting

### Issue: The checks disagree

Identifying:
One script reports 0 findings and another reports many for the same files (as the cohesion and link checks did on 2026-11-21).

Solution:
Each script checks something narrower than the Rule. Read the conflicting finding, decide which convention is in force (for example the `.praxis/`-prefixed links of the list files), and record the convention question as needing consent; do not silence one script to match the other.

### Issue: A fix would touch a domain item

Identifying:
The correct form is clear, but the file is under `.praxis/domains/`.

Solution:
Do not fix it. Record it as a proposal, with the exact change, for `praxis-flow-learn`.

### Issue: Too many findings to read

Identifying:
A script reports more findings than can be read one by one.

Solution:
Group them by cause (as 143 list-file links shared one cause), read one of each group, and record the group as one finding with its count.

## Notes

The narrow form of this check is step 8 of `praxis-flow-introspect`; that skill can call this one instead of repeating it.
