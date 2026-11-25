# Praxis Flow

A process for planning an agent's actions, reflecting on them, and improving its behavior.

Praxis rests on three ideas: learning comes from action, from reflection on what happened, and from honest knowledge of oneself. An agent that follows it writes down what it expects before it acts, compares that with what happened, and lets the difference change what it believes and does next time.

This is the `template/semantic` branch: the working plumbing (the flow, skills, lifecycles, templates, and state) with only the domain items that plumbing needs. Copy it into a project to start from there.

## Contents

- [How the Flow Runs](#how-the-flow-runs)
- [Getting Started](#getting-started)
- [Key Terms](#key-terms)
- [Directory Structure](#directory-structure)

## How the Flow Runs

Every user prompt goes through the Flow, which is described in full in `.praxis/flow.md`. Each step is a skill named `praxis-flow-<step>`; `praxis-flow-entry` reads the current state and says which step comes next.

1. **Plan**: `praxis-flow-decompose` splits the prompt into Tasks, and `praxis-flow-plan` groups them into Plans.
2. **Anticipate**: `praxis-flow-predict` writes what each Plan is expected to cause, and `praxis-flow-discern` approves, revises, or rejects the Plan before anything is done.
3. **Act**: `praxis-flow-act` performs each Approved Plan and records an Outcome.
4. **Reflect**: `praxis-flow-analyze` compares each Outcome with its Prediction, `praxis-flow-learn` decides what to change in the domains and tracking, and `praxis-flow-record` commits it.
5. **Return**: `praxis-flow-report` summarizes the run for the user, then `praxis-flow-clear-state` clears the state.

The Flow is not strictly linear: a rejected or revised Plan sends it back to planning. When every Task is trivial, the Plan, Prediction, and Outcome are written nearly empty instead of the steps being skipped.

## Getting Started

Add a copy of `.praxis` to the root of your project workspace, then use your favorite tool to ask your favorite model to incorporate `.praxis` into your project.

## Key Terms

- **Task**: something the user asked for.
- **Plan**: an ordered list of steps that completes one or more Tasks.
- **Prediction**: what a Plan is expected to cause, written before the Plan is performed.
- **Outcome**: what happened when the Plan was performed.
- **Analysis**: the comparison of an Outcome with its Prediction.
- **Domain item**: a belief, environment, expectation, intention, opinion, practice, principle, rule, or value that guides the agent.
- **Factory product**: an agent, habit, hook, pattern, script, skill, or tool the agent can use or make.

`.praxis/state/README.md` describes the state types, `.praxis/domains/README.md` the domain items, and `.praxis/factory/README.md` the factory products. `.praxis/glossary.md` is reserved for the other terms and is empty on this branch.

## Directory Structure

`.praxis/`: Base directory for everything related to Praxis Flow

`.praxis/flow.md`: The Praxis Flow overview

`.praxis/glossary.md`: Definitions for key Praxis Flow terms

`.praxis/domains/`: Domains of items (beliefs, environment, expectations, intentions, opinions, practices, principles, rules, values); Asserted items are enforced

`.praxis/factory/`: The Factory: agents, habits, hooks, patterns, scripts, skills, and tools, with their READMEs and lists

`.praxis/factory/skills/`: All skills, including the Flow skills (`praxis-flow-*`); an installed skill is moved to `.claude/skills/<name>/` and recorded in `.praxis/factory/installs.yaml`

`.praxis/lifecycles/`: State-machine grammars for each component

`.praxis/state/`: State tracking for each run through the Praxis Flow

`.praxis/templates/`: Templates for all aspects of the Praxis Flow

`.praxis/tracking/`: Confidence tables, Signals, and introspections (`introspections.md` and `introspections/`) for the quality of the domains, the factory, and the Praxis Flow itself
