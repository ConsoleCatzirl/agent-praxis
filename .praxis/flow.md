# Agent Praxis Flow

Learning from our actions.

A self-improving agent framework built on the axioms that learning comes from action, reflection, and honest self-knowledge.

The flow is not strictly linear, some conditions may cause flow to return to earlier phases before proceeding.
One framing is as a state machine; another is a grammar; and yet another is a flow chart.

## The Praxis Flow

There are Phases, each with its own flow:

Anticipate -> Act -> Reflect

Use `praxis-entry` for entry or re-entry.

### Anticipate

`praxis-decompose` ->  [ `praxis-plan` | Act | Reflect ]
`praxis-plan` -> `praxis-predict`
`praxis-predict` -> [ `praxis-plan` | `praxis-discern` ] 
`praxis-discern` -> [ `praxis-plan` | Act | Reflect ]

### Act

`praxis-flow-act` -> Reflect

### Reflect

`praxis-analyze` -> `praxis-learn` 
`praxis-learn` -> `praxis-record`
`praxis-record` -> `praxis-report`
`praxis-report` -> End
