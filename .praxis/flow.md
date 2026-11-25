# Agent Praxis Flow

Learning from our actions.

A self-improving agent framework built on the axioms that learning comes from action, reflection, and honest self-knowledge.

The flow is not strictly linear, some conditions may cause flow to return to earlier phases before proceeding.
One framing is as a state machine; another is a grammar; and yet another is a flow chart.

## The Praxis Flow

There are Phases, each with its own flow:

Anticipate -> Act -> Reflect

Use `praxis-flow-entry` for entry or re-entry.

### Anticipate

`praxis-flow-decompose` -> [ `praxis-flow-plan` | Act | Reflect ]
`praxis-flow-plan` -> `praxis-flow-predict`
`praxis-flow-predict` -> [ `praxis-flow-plan` | `praxis-flow-discern` ]
`praxis-flow-discern` -> [ `praxis-flow-plan` | Act | Reflect ]

### Act

`praxis-flow-act` -> Reflect

### Reflect

`praxis-flow-analyze` -> `praxis-flow-learn`
`praxis-flow-learn` -> `praxis-flow-record`
`praxis-flow-record` -> `praxis-flow-report`
`praxis-flow-report` -> `praxis-flow-clear-state` -> End

`praxis-flow-clear-state` is the last tool call of `praxis-flow-report`, after `praxis-flow-verify-state` confirms the iteration is complete.

## Outside the Flow

- `praxis-flow-introspect`: deep analysis across all runs, run as a Pattern inside a Plan.
- `praxis-flow-self-review`: ad-hoc self-assessment between `praxis-flow-learn` and `praxis-flow-introspect`.
- `praxis-create-*`, `praxis-refine-*`, `praxis-promote-*`: create, change, and promote domain items and factory products (see `.praxis/domains/README.md` and `.praxis/factory/README.md`).
