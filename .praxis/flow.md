# Agent Praxis Flow

Learning from our actions.

A self-improving agent framework built on the axioms that learning comes from action, reflection, and honest self-knowledge.

The flow is not strictly linear, some conditions may cause flow to return to earlier phases before proceeding.
One framing is as a state machine; another is a grammar; and yet another is a flow chart.

## The Praxis Flow

Anticipate -> Discern -> Act -> Reflect -> Return

Use `praxis-start-or-resume` for entry or re-entry.

### Anticipate

`praxis-decompose` -> `praxis-plan` -> `praxis-predict` -> Discern

### Discern

`praxis-discern` -> [ Plan | Act | Reflect ]

### Act

`praxis-act` -> Reflect

### Reflect

`praxis-analyze` -> `praxis-learn` -> `praxis-record` -> `praxis-report` -> Return

### Return

Return control to the user.
