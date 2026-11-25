---
name: praxis-create-hook
description: Create a new hook in `.praxis/factory/hooks/`, right-sized to its complexity, with its README, list entry, and starting confidence, and commit it. Use when a Plan or Task needs a hook that does not exist.
confidence: Low
complexity: Qualitative
---

# Skill: Praxis Create Hook

Create a new hook in the factory: a custom Claude Code hook (a command the harness runs on an event such as a tool call).

## Origin
Taken from the workspace's skill of the same name, without its run evidence; no recorded use on this branch.

## Purpose
Add a hook that is right-sized to its purpose, recorded in the factory list and the confidence table, and starts Unstable until use earns it confidence.

## When to Use
When `praxis-flow-plan` finds that no existing factory product, Pattern, or skill can address a Task and a new hook is the right size of solution. Check `.praxis/factory/hooks.md` first; if a hook exists that nearly fits, use `praxis-refine-hook` instead. A hook here is an agent hook: a Claude Code hook the harness runs on an event. A git hook, or a check run by path, is a script: use `praxis-create-script`.

## How it Works
The skill states the hook's purpose and complexity, builds it, tests it, documents it in its README, lists it in `.praxis/factory/hooks.md`, and adds its row to `.praxis/tracking/confidence/hooks.csv` at Unstable and Low (the factory lifecycle's New to Unstable). It does not promote or register it.

## Requirements
- A Task or Plan that needs the hook, and the user's consent where the Plan requires it.
- Complexity: Regex or Mechanical (a hook is a script; keep it deterministic and fast).
- `.praxis/factory/README.md`, `.praxis/factory/hooks/README.md`, and `.praxis/lifecycles/factory-lifecycle.md` have been read.

## Inputs
The purpose of the hook, a short name (lowercase, hyphenated, prefixed `praxis-` for skills only), and its intended callers.

## Procedure
1. Read the following files if they are not already in context: `.praxis/factory/README.md`, `.praxis/factory/hooks/README.md`, `.praxis/factory/hooks.md`, and `.praxis/lifecycles/factory-lifecycle.md`.
2. Check that no hook of that name or purpose is listed in `.praxis/factory/hooks.md`. If one is, stop and refine it instead.
3. State the purpose in one sentence and choose the complexity level.
4. Check `.praxis/factory/` for existing products to reuse before writing anything new.
5. Create the directory `.praxis/factory/hooks/${hook}/`.
6. Name the event (for example PreToolUse, PostToolUse, UserPromptSubmit, Stop) and the matcher, and say what the hook enforces or records and what it must never block.
7. Implement the hook as a script at `.praxis/factory/hooks/${hook}/${hook}.sh` (or `.py`), right-sized by the complexity levels in `.praxis/factory/README.md`. It reads the event JSON on stdin and exits 0 to allow, or with the blocking status the harness defines, with the reason on stderr.
8. Make it fail open: a crash, a missing file, or malformed input must not block the user's work unless blocking is the point of the hook.
9. Test it by piping at least one allowing, one blocking, and one malformed event into it, and record the commands and results.
10. Write `.praxis/factory/hooks/${hook}/README.md` from `.praxis/templates/factory-product-template.md`: event, matcher, purpose, exit-code behavior, tests, and conditions for revision.
11. Register the hook with the `add-item` script of the workspace (not on this branch: do the step by hand): it adds the hook to `.praxis/factory/hooks.md` in alphabetical order, linking to its README, and a row to `.praxis/tracking/confidence/hooks.csv` (`hook,confidence,lifecycle,…,current-plan-count,total-plan-count,version`) at `Unstable`, `Low`, plan counts `0` and revision count `1`.
12. Commit the hook, its README, the list, and the table row as one logical change with `git`.

## Output
A new hook under `.praxis/factory/hooks/${hook}/` with a README (from `.praxis/templates/factory-product-template.md`), a list entry, a tracking row at Unstable and Low, and a commit. The hook is not registered while it is Unstable. Registering it in the project's Claude settings file or `.claude/settings.local.json` is a separate step that needs the user's approval; use the `update-config` skill for it.

## Success Criteria
- The hook does what its README says, shown by the recorded test or trial.
- The list entry, README, and tracking row all exist and agree on the name.
- The complexity level is stated and is the smallest that works.
- Nothing is registered, linked, or promoted without the user's approval.

## Domain Alignment

None recorded yet; the domain lists are still being populated.

## Related Skills

- praxis-refine-hook
- praxis-create-script
- praxis-create-skill
- praxis-promote-factory
- praxis-flow-plan

## Troubleshooting

### Issue: A smaller solution would do

Identifying:
The hook would only wrap one command or one pattern that already exists.

Solution:
Use the existing product in the Plan or Pattern, and do not add the hook.

### Issue: The test cannot be run safely

Identifying:
Testing the hook would change files, settings, or services outside `.praxis/factory/`.

Solution:
Test against a copy or a temporary directory in the scratchpad, and record what was and was not exercised in the README.
