---
name: praxis-create-agent
description: Create a new agent in `.praxis/factory/agents/`, right-sized to its complexity, with its README, list entry, and starting confidence, and commit it. Use when a Plan or Task needs a agent that does not exist.
confidence: Low
complexity: Qualitative
---

# Skill: Praxis Create Agent

Create a new agent in the factory: a custom agent definition (a delegate with its own prompt, tools, model and effort).

## Origin
Praxis Template

## Purpose
Add a agent that is right-sized to its purpose, recorded in the factory list and the confidence table, and starts Unstable until use earns it confidence.

## When to Use
When `praxis-flow-plan` finds that no existing factory product, Pattern, or skill can address a Task and a new agent is the right size of solution. Check `.praxis/factory/agents.md` first; if a agent exists that nearly fits, use `praxis-refine-agent` instead.

## How it Works
The skill states the agent's purpose and complexity, builds it, tests it, documents it in its README, lists it in `.praxis/factory/agents.md`, and adds its row to `.praxis/tracking/confidence/agents.csv` at Unstable and Low (the factory lifecycle's New to Unstable). It does not promote or register it.

## Requirements
- A Task or Plan that needs the agent, and the user's consent where the Plan requires it.
- Complexity: Qualitative (an agent exists because the work needs judgment; if the work is mechanical, create a script instead).
- `.praxis/factory/README.md`, `.praxis/factory/agents/README.md`, and `.praxis/lifecycles/factory-lifecycle.md` have been read.

## Inputs
The purpose of the agent, a short name (lowercase, hyphenated, prefixed `praxis-` for skills only), and its intended callers.

## Procedure
1. Read the following files if they are not already in context: `.praxis/factory/README.md`, `.praxis/factory/agents/README.md`, `.praxis/factory/agents.md`, and `.praxis/lifecycles/factory-lifecycle.md`.
2. Check that no agent of that name or purpose is listed in `.praxis/factory/agents.md`. If one is, stop and refine it instead.
3. State the purpose in one sentence and choose the complexity level.
4. Check `.praxis/factory/` for existing products to reuse before writing anything new.
5. Create the directory `.praxis/factory/agents/${agent}/`.
6. Write the agent's single responsibility in one sentence. If it has two, make two agents.
7. Choose the model and effort from `.praxis/tracking/confidence/praxis-stage-models.csv` when the agent serves a Flow stage; otherwise start with the cheapest model that plausibly fits and record why.
8. Grant the fewest tools the responsibility needs. Prefer read-only tools; an agent that writes needs a stated reason.
9. Write the agent definition as `.praxis/factory/agents/${agent}/${agent}.md` with Claude Code agent frontmatter (`name`, `description`, `tools`, `model`) and a prompt that states the inputs it receives, the output format it returns, and what it must not do.
10. Write `.praxis/factory/agents/${agent}/README.md` from `.praxis/templates/factory-product-template.md`: purpose, origin, model and effort, tools and why, input and output contract, and conditions for revision.
11. Register the agent: add the agent to `.praxis/factory/agents.md` in alphabetical order, linking to its README, and a row to `.praxis/tracking/confidence/agents.csv` (`agent,model,effort,confidence,lifecycle,…,current-plan-count,total-plan-count,version`) at `Unstable`, `Low`, plan counts `0` and revision count `1`. Then fill in the model and effort in the row.
12. Install it as the install lifecycle describes, and set `installed` to `Installed` in its row: agents are installed from Low, a standing exception of the owner's (`.praxis/lifecycles/install-lifecycle.md`).
13. Commit the agent's README, the list, `installs.yaml`, and the table row as one logical change with `git`, and the installed file in `.claude/agents/<name>.md` in the workspace repository.

## Output
A new agent installed at `.claude/agents/${agent}.md` and recorded in `.praxis/factory/installs.yaml`, with its README (from `.praxis/templates/factory-product-template.md`) in `.praxis/factory/agents/${agent}/`, a list entry, a tracking row at Unstable, Low and Installed, and commits in both repositories.

## Success Criteria
- The agent does what its README says, shown by the recorded test or trial.
- The list entry, README, and tracking row all exist and agree on the name.
- The complexity level is stated and is the smallest that works.
- It is installed under the standing exception for agents; nothing else is registered or promoted without the user's approval.

## Domain Alignment

None recorded yet; the domain lists are still being populated.

## Related Skills

- praxis-refine-agent
- praxis-create-script
- praxis-create-skill
- praxis-promote-factory
- praxis-flow-plan

## Troubleshooting

### Issue: A smaller solution would do

Identifying:
The agent would only wrap one command or one pattern that already exists.

Solution:
Use the existing product in the Plan or Pattern, and do not add the agent.

### Issue: The test cannot be run safely

Identifying:
Testing the agent would change files, settings, or services outside `.praxis/factory/`.

Solution:
Test against a copy or a temporary directory in the scratchpad, and record what was and was not exercised in the README.
