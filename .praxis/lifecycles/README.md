# Praxis Lifecycles

## Lifecycle Templates

Lifecycles are created from one of the the templates at 
`.praxis/templates/confidence-lifecycle-template.md` or `.praxis/templates/state-lifecycle-template.md`

## Confidence Levels

Domain and factory lifecycles track confidence levels for stage promotion.
The confidence lifecycle can be found in `.praxis/lifecycles/confidence-lifecycle.md`.

## Implicit Stages

Two stages implicitly exist for all lifecycles:
* **New**: Start state; initial creation.
* **Cleared**: Removal; end state.

## Domain Lifecycles

These lifecycles are created from the template at `.praxis/templates/confidence-lifecycle-template.md`,
and cover the items in `.praxis/domains/`.

* [Assertion Lifecycle](assertion-lifecycle.md)
* [Evidence-Based Lifecycle](evidenced-lifecycle.md)

## Factory Lifecycle

This lifecycle is created from the template at `.praxis/templates/confidence-lifecycle-template.md`,
and cover the items in `.praxis/factory/`.

* [Factory Lifecycle](factory-lifecycle.md)

## State Lifecycles

These lifecycles are created from the template at `.praxis/templates/state-lifecycle-template.md`,
and cover the items in `.praxis/state/`.

* [Task Lifecycle](task-lifecycle.md)
* [Plan Lifecycle](plan-lifecycle.md)
* [Prediction Lifecycle](prediction-lifecycle.md)
* [Outcome Lifecycle](outcome-lifecycle.md)
* [Analysis Lifecycle](analysis-lifecycle.md)

