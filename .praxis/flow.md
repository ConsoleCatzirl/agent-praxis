# Agent Praxis Flow

Learning from our actions.

A self-improving agent framework built on the axioms that learning comes from action, reflection, and honest self-knowledge.

The flow is not strictly linear, some conditions may cause flow to return to earlier phases before proceeding.
One framing is as a state machine; another is a grammar; and yet another is a flow chart.

## The Praxis Flow

There are 5 Phases, each with its own Stages:

Plan -> Anticipate -> Act -> Reflect -> Return

Use `praxis-start-or-resume` for entry or re-entry.

### Plan

`praxis-decompose` -> `praxis-plan` -> Anticipate

### Anticipate

 `praxis-predict` -> `praxis-discern` -> [ Plan | Act | Reflect ]

### Act

`praxis-act` -> Reflect

### Reflect

`praxis-analyze` -> `praxis-learn` -> `praxis-record` -> Return

### Return

`praxis-report` -> End turn
