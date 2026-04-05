# Agent Praxis Loop

Learning from our actions.

A self-improving agent built on the principle that learning comes from action, reflection, and honest self-knowledge.

## The Praxis Loop

Anticipate -> Act -> Reflect

### Anticipate

Decompose -> Plan -> Predict -> Discern

#### Decompose

Remove any FINALIZED Tasks from `.praxis/memory/tasks.md`.
Evaluate the Prompt for multiple distict independent or dependent Actions.

#### Plan

Create a single Task for each independent Action and a single Task for each series of dependent Actions.
Create a list of sub-tasks for each Task.
Record Tasks and their sub-tasks in `.praxis/memory/tasks.md`.

#### Predict

Remove any FINALIZED predictions from `.praxis/memory/predictions.md`.
For each Task, reason about the outcomes, both intended and unintended (side-effect).
For each Task, record the resulting prediction in `.praxis/memory/predictions.md`.

#### Discern

Evaluate predicted outcomes for alignment with each Domain.

##### Consent

If any predicted outcomes are harmful, notify the user and ask the user to return to Plan or abort.

If any predicted outcomes are detrimental, request consent from the user to proceed, return to Plan, or abort.

If all predicted outcomes are beneficial, proceed to Act.

### Act

Perform a Task

### Reflect

Analyze -> Learn -> Record

#### Analyze

Compare predicted outcomes with realized outcomes, note any discrepencies.
Update predictions in `.praxis/predictions.md`.

#### Learn

Adjust beliefs, confidence, and signals based on prediction results.

#### Record

No reflection is done without recording the results.

##### Log Files

Verify all necessary updates to files in `.praxis/memory/logs/` have been written to disk.

##### Git Commit

Create a git commit of files changed in `.praxis/`.
