---
name: praxis-flow-self-review
description: Ad-hoc self-assessment of the agent's recent behavior against the domains, the Flow, and recent Outcomes, at a depth between praxis-flow-learn and praxis-flow-introspect. Use when the user asks the agent to reflect, or after a surprise, correction, or harmful outcome that should not wait for the next learn or introspection.
confidence: Low
complexity: Qualitative
---

# Skill: Praxis Flow Self-Review

Assess the agent's own recent behavior, on request or after something notable, without a full history sweep.

## Origin
Taken from the workspace's skill of the same name, without its run evidence; no recorded use on this branch.

## Purpose
Notice, soon and cheaply, where recent actions and their stated rationale departed from the domains, the Flow, or the Predictions, and say what should change.

## When to Use
- The user asks the agent to reflect, check itself, or look back at what just happened.
- A correction, a surprise, or a harmful outcome occurs and waiting for `praxis-flow-learn` (end of run) or `praxis-flow-introspect` (many runs) would lose the detail.
Not for a full review of the current run's Analyses (`praxis-flow-learn`) or a trend across many runs (`praxis-flow-introspect`).

## How it Works
`praxis-flow-learn` looks at this run's Analyses; `praxis-flow-introspect` looks at the whole history. This skill looks at a bounded window in between: the current run so far, plus at most the last few completed runs, and the domain items and factory products those runs relied on. It compares what the agent did and said with what the domains and Predictions required, and reports. It proposes changes; it does not make domain changes and does not count as a run's Learn stage.

## Requirements
Something to reflect on: state in `.praxis/state/`, a recent conversation, or committed state of recent runs. If there is none, say so.

## Inputs
- The window: by default the current run and the last three `Clear state` commits of `.praxis/`; narrowed or widened by the user.
- State items in the window: Tasks, Plans, Predictions, Outcomes, Analyses (`.praxis/state/`, and earlier runs via `git show <commit>~1:state/...`).
- The domain items and factory products those items name.
- Optionally a focus from the user (a decision, a behavior, a feeling that something went wrong).

## Procedure
1. Fix the window and the focus, and state them.
2. Read the state items in the window. For each Plan, compare Prediction and Outcome: what was predicted, what happened, and whether the difference was anticipated.
3. Check the agent's behavior against the domains it cited and the ones it did not. Read `.praxis/domains/*.md` and the items most relevant to the focus, and note every item that was violated, set aside without a recorded reason, or stretched.
4. Check the agent's behavior against the Flow: were the stages followed in order, were the templates filled in, was each domain change judged case by case and named in the review, and was consent obtained where a factory promotion needed it?
5. Look at the rationale, not just the result: where did the agent state a belief or expectation that the evidence did not support, act on an unverified premise, or do more or less than the Task asked?
6. Check the confidence of the factory products used (`.praxis/tracking/confidence/*.csv`): were any trusted beyond their confidence, or did any behave in a way that argues for a change?
7. For each finding, write: what happened, the evidence (state file, commit, or conversation turn), the domain item or Flow rule it bears on, and its strength (Weak, Moderate, or Strong). A single observation is Weak.
8. Triage each finding as:
   - **Fix now**: a mistake in the current work that can be corrected immediately; do it and say so.
   - **Propose**: a tracking change, a domain change, or a factory refinement (`praxis-refine-*`) for the user's consent, or for `praxis-flow-learn` to include in its review.
   - **Note only**: too weak to act on.
9. Report the result to the user briefly, leading with what the agent got wrong or is unsure of. If the reflection happens inside a Plan, record it as that Plan's Outcome.

10. Check the facts of the steps above by reading the run history (recent runs, and the owner's prompts and side questions since the window's start) and by checking conformance.

## Output
A short self-assessment: the window, the findings with evidence and strength, and the triage. Written to the Outcome when run inside a Plan, otherwise given to the user. No domain item is changed.

## Success Criteria
- The window and focus are stated.
- Each finding cites evidence, and a window with no findings says "none found".
- Departures from the domains or the Flow are named, not softened, including those the agent had not recorded itself.
- No factory product was promoted without the user's consent, and every domain change was named in the review.

## Domain Alignment

None recorded yet; the domain lists are still being populated.

## Related Skills

- praxis-flow-learn
- praxis-flow-introspect
- praxis-flow-analyze
- praxis-refine-skill
- praxis-promote-evidenced

## Troubleshooting

### Issue: Nothing in the window

Identifying:
The state is empty and no recent run is committed.

Solution:
Say that there is nothing to assess, and ask the user for a focus, or use the conversation itself as the window.

### Issue: The finding is a trend

Identifying:
The same departure appears in more than one run in the window.

Solution:
Record it as a candidate for `praxis-flow-introspect`; do not propose a Pattern or Signal from three runs of one author.

### Issue: The finding is a flaw in a skill, not in the agent

Identifying:
Following the skill as written led to the wrong result.

Solution:
Propose a change with `praxis-refine-skill` and cite the step; do not work around it silently.
