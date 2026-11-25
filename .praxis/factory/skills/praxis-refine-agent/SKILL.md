---
name: praxis-refine-agent
description: Modify an existing agent in `.praxis/factory/agents/` with the smallest change that fits the reason, retest it, update its README and confidence row, and commit. Use when a agent's behavior needs fixing or extending.
confidence: Low
complexity: Qualitative
---

# Skill: Praxis Refine Agent

Iteratively improve an existing agent (a custom agent definition (a delegate with its own prompt, tools, model and effort)).

## Origin
Praxis Template

## Purpose
Change a agent while keeping it tested, documented, and honestly tracked, so that its confidence reflects what it does now.

## When to Use
When an Outcome, Analysis, introspection, or the user shows that a agent is wrong, incomplete, or no longer right-sized. Not for adding a new agent; use `praxis-create-agent`.

## How it Works
The skill classifies the change, makes the smallest edit, re-runs the agent's tests, updates its README, and adjusts the lifecycle and confidence in `.praxis/tracking/confidence/agents.csv` by the factory lifecycle: a major revision (`.praxis/glossary.md`, "Major revision") lowers its confidence one level (High to Medium) and keeps its stage (the hysteresis at Medium), and its current plan count restarts with the new revision.

## Requirements
- An existing agent listed in `.praxis/factory/agents.md`, with its README.
- A stated reason for the change.

## Inputs
The agent's name and the reason for the change.

## Procedure
1. Read the following files if they are not already in context: `.praxis/factory/README.md`, `.praxis/factory/agents/${agent}/README.md`, the agent's own files, its row in `.praxis/tracking/confidence/agents.csv`, and `.praxis/lifecycles/factory-lifecycle.md`.
2. If another factory product already addresses the reason, use it in the agent instead of adding code to the agent.
3. Classify the change:
   - **Fix** (the agent does not do what its README says): correct it, and add a test that would have caught it.
   - **Extension** (it should do more): add the minimum; if the purpose would no longer fit in one sentence, create a second agent instead.
   - **Model or effort change**: change one of them at a time, and record the reason; when the agent serves a Flow stage also update `.praxis/tracking/confidence/praxis-stage-models.csv`.
   - **Tool change**: add a tool only with a stated reason; removing one is always safe to try first.
4. If another factory product must change too, create a Task and a Plan for that change instead of editing it here.
5. Make the change, then re-run the agent's recorded tests. Report any test that fails; do not weaken a test to make it pass.
6. Update the README (`.praxis/templates/factory-product-template.md`; refresh `modified`, Status, Confidence): purpose, interface or behavior, tests, and conditions for revision.
7. Update the row in `.praxis/tracking/confidence/agents.csv` (`agent,model,effort,confidence,lifecycle,…,current-plan-count,total-plan-count,version`): When the confidence or stage changes, change the file and the row together, and make only a move the lifecycles give.
   - A major revision of a agent at High lowers it to Medium (a minor or patch revision changes no confidence); it stays Stable, since the stage changes only when confidence leaves Medium (factory lifecycle).
   - An Unstable agent stays Unstable; lower its confidence one level if the change was a fix for a harmful outcome (see `.praxis/lifecycles/confidence-lifecycle.md`).
   - Leave the plan and revision counts to Learn, which writes them from history: this change, once committed, raises its version by its kind, and only a major revision resets its current count.
8. Stage the change and run the checks that Pattern: Refine a Praxis Component requires before a commit (the checks above and the tests of any staged script); on a failure, fix the cause and check again, and do not commit until it passes. Then commit the change, the README, and the tracking row as one logical change with `git`, giving the reason in the message. The commit carries the trailer of its kind: `Revision: breaking` for a major revision, `Revision: feature` for a minor one, and `Revision: fix` or none for a patch (`.praxis/glossary.md`, "Major revision").

## Output
A modified agent, retested, with an updated README and confidence row, and a commit.

## Success Criteria
- The change matches the stated reason and nothing more.
- The agent's tests pass, and a fix has a new test.
- The README and tracking row agree with the agent.
- The lifecycle and confidence are a legal move in `.praxis/lifecycles/factory-lifecycle.md`.

## Domain Alignment

None recorded yet; the domain lists are still being populated.

## Related Skills

- praxis-create-agent
- praxis-promote-factory
- praxis-flow-analyze
- praxis-flow-learn

## Troubleshooting

### Issue: Callers depend on the old behavior

Identifying:
`grep -rn` of the agent's name in `.praxis/` and `.claude/` finds users that the change would break.

Solution:
Keep the old behavior behind the old interface, or create a Task and Plan to update each caller in the same commit.

### Issue: The change is larger than a refinement

Identifying:
The purpose no longer fits in one sentence, or most of the agent is being rewritten.

Solution:
Create a new agent with `praxis-create-agent`, and retire the old one through the factory lifecycle with the user's consent.
