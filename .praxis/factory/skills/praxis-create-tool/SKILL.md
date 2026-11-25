---
name: praxis-create-tool
description: Create a new tool in `.praxis/factory/tools/`, right-sized to its complexity, with its README, list entry, and starting confidence, and commit it. Use when a Plan or Task needs a tool that does not exist.
confidence: Low
complexity: Qualitative
---

# Skill: Praxis Create Tool

Create a new tool in the factory: a custom MCP tool (a tool exposed to the agent through the Model Context Protocol, with a defined input schema and output, wrapping one or more scripts).

## Origin
Taken from the workspace's skill of the same name, without its run evidence; no recorded use on this branch.

## Purpose
Add a tool that is right-sized to its purpose, recorded in the factory list and the confidence table, and starts Unstable until use earns it confidence.

## When to Use
When `praxis-flow-plan` finds that no existing factory product, Pattern, or skill can address a Task and a new tool is the right size of solution. Check `.praxis/factory/tools.md` first; if a tool exists that nearly fits, use `praxis-refine-tool` instead. A tool here is an MCP tool: one the agent calls through a Model Context Protocol server. A command-line program or a library is a script: use `praxis-create-script`.

## How it Works
The skill states the tool's purpose and complexity, builds it, tests it, documents it in its README, lists it in `.praxis/factory/tools.md`, and adds its row to `.praxis/tracking/confidence/tools.csv` at Unstable and Low (the factory lifecycle's New to Unstable). It does not promote or register it.

## Requirements
- A Task or Plan that needs the tool, and the user's consent where the Plan requires it.
- Complexity: Mechanical or Structural (an MCP tool wraps scripts behind a stable, schema-defined interface).
- `.praxis/factory/README.md`, `.praxis/factory/tools/README.md`, and `.praxis/lifecycles/factory-lifecycle.md` have been read.

## Inputs
The purpose of the tool, a short name (lowercase, hyphenated, prefixed `praxis-` for skills only), and its intended callers.

## Procedure
1. Read the following files if they are not already in context: `.praxis/factory/README.md`, `.praxis/factory/tools/README.md`, `.praxis/factory/tools.md`, and `.praxis/lifecycles/factory-lifecycle.md`.
2. Check that no tool of that name or purpose is listed in `.praxis/factory/tools.md`. If one is, stop and refine it instead.
3. State the purpose in one sentence and choose the complexity level.
4. Check `.praxis/factory/` for existing products to reuse before writing anything new.
5. Create the directory `.praxis/factory/tools/${tool}/`.
6. Define the interface first: the tool name, a description the agent can choose it by, the JSON input schema (types, required fields, defaults), the output content, and the error shape.
7. Reuse existing factory scripts for the work and wrap them; write a new script with `praxis-create-script` only for what no script does.
8. Implement the MCP server code at `.praxis/factory/tools/${tool}/` (one server per directory; stdio transport unless the user asks otherwise). The tool validates its arguments against its schema, does one thing, and is idempotent when it writes.
9. Test it with valid, invalid, and empty input, through a client or an MCP tool-call request, and record the commands and results.
10. Write `.praxis/factory/tools/${tool}/README.md` from `.praxis/templates/factory-product-template.md`: the interface (schema and output), the scripts it wraps, how to start the server, tests, and conditions for revision.
11. Register the tool with the `add-item` script of the workspace (not on this branch: do the step by hand): it adds the tool to `.praxis/factory/tools.md` in alphabetical order, linking to its README, and a row to `.praxis/tracking/confidence/tools.csv` (`tool,confidence,lifecycle,…,current-plan-count,total-plan-count,version`) at `Unstable`, `Low`, plan counts `0` and revision count `1`.
12. Commit the tool, its README, the list, and the table row as one logical change with `git`.

## Output
A new tool under `.praxis/factory/tools/${tool}/` with a README (from `.praxis/templates/factory-product-template.md`), a list entry, a tracking row at Unstable and Low, and a commit. The tool stays under `.praxis/factory/tools/`. Registering the server with the harness (an MCP server entry in `.mcp.json` or settings, and a permission entry) needs the user's approval; use the `update-config` skill.

## Success Criteria
- The tool does what its README says, shown by the recorded test or trial.
- The list entry, README, and tracking row all exist and agree on the name.
- The complexity level is stated and is the smallest that works.
- Nothing is registered, linked, or promoted without the user's approval.

## Domain Alignment

None recorded yet; the domain lists are still being populated.

## Related Skills

- praxis-refine-tool
- praxis-create-script
- praxis-create-skill
- praxis-promote-factory
- praxis-flow-plan

## Troubleshooting

### Issue: A smaller solution would do

Identifying:
The tool would only wrap one command or one pattern that already exists.

Solution:
Use the existing product in the Plan or Pattern, and do not add the tool.

### Issue: The test cannot be run safely

Identifying:
Testing the tool would change files, settings, or services outside `.praxis/factory/`.

Solution:
Test against a copy or a temporary directory in the scratchpad, and record what was and was not exercised in the README.
