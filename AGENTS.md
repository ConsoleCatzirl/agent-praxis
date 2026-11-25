# Agent Behavior

## Praxis Flow
All agent behavior must follow the Praxis Flow found at `.praxis/flow.md`.
See `README.md` for more information.

Begin every user prompt by invoking `praxis-flow-entry`; it determines which phase and skill to continue with. Every prompt is decomposed into Tasks; when all of them are trivial, the Plan, Prediction, and Outcome are Bypassed (near-empty) instead of the stages being skipped. The flow ends with `praxis-flow-report`, which returns control to the user.

Phases: Plan (`praxis-flow-decompose`, `praxis-flow-plan`) -> Anticipate (`praxis-flow-predict`, `praxis-flow-discern`) -> Act (`praxis-flow-act`) -> Reflect (`praxis-flow-analyze`, `praxis-flow-learn`, `praxis-flow-record`) -> Return (`praxis-flow-report`, which ends by clearing the state with `praxis-flow-clear-state`).

### Domains
Domain items live in `.praxis/domains/` (beliefs, environment, expectations, intentions, opinions, practices, principles, rules, values); see `.praxis/domains/README.md`.
Items in the Asserted stage (assertion lifecycle) are enforced: they MUST be adhered to AT ALL TIMES, and a violation or exception must be documented with its rationale in the Analysis. Rules carry their own RFC 2119 keyword (MUST or SHOULD) and are enforced as written. Items in other stages, and evidence-based items (beliefs, environment, expectations), inform anticipation and are weighed by their confidence.
If two Asserted items contradict, do not choose between them: resolve the contradiction by dialectical synthesis (see `.praxis/glossary.md`), proposed to the user for consent.

## Working Rules

### State
- Current-run state lives in `.praxis/state/`: tasks, plans, predictions, outcomes, and analyses. Write each using its template in `.praxis/templates/`.
- Update an item's status as it moves through its lifecycle in `.praxis/lifecycles/`. Do not skip stages.
- To change a Plan, mark it and its Prediction Rejected with a note beginning `Revise:` and write a new Plan that cites it in its Notes; do not edit or delete Rejected items.
- Do not act on a Plan until its Prediction has been Approved by `praxis-flow-discern`; a Bypass Plan, whose Tasks are all trivial, is the exception.
- Clear state with `praxis-flow-clear-state` at the end of each run, after the run has been recorded, or when the user asks to start fresh or to abandon the run.

### Domain and Tracking Changes
- Adding, changing, or removing an item in `.praxis/domains/` is a judgement case by case: make the change when the owner asks for it, or when it is small and backed by recorded evidence; otherwise propose it in the `praxis-flow-learn` review and wait for the owner. Either way, name every domain change in that review.
- Update confidence levels, patterns, and signals in `.praxis/tracking/` based on analyzed outcomes, following `.praxis/lifecycles/confidence-lifecycle.md`.
- If an Asserted domain item is violated, or set aside, record it in the Analysis.

### Skills and the Factory
- Praxis skills live in `.praxis/factory/skills/<name>/SKILL.md`; the directory name, the `name` in the frontmatter, and the name used in other files are the same. A skill is installed by moving it to `.claude/skills/<name>/`, with nothing left in `.praxis/factory/skills/` and the move recorded in `.praxis/factory/installs.yaml`, when its confidence reaches the level the install lifecycle gives (`.praxis/lifecycles/install-lifecycle.md`).
- New factory products (agents, habits, hooks, patterns, scripts, skills, tools) are created with `praxis-create-<type>` and start Unstable at Low confidence. Do not promote them without user approval, per `.praxis/lifecycles/factory-lifecycle.md` and `praxis-promote-factory`.

### Commits
- Every stage commits what it changed under `.praxis/` when it ends, one commit per logical change.

## Reference
- `.praxis/README.md`: directory structure
- `.praxis/glossary.md`: terminology
- `.praxis/lifecycles/`: allowed stages and transitions for each component
- `.praxis/templates/`: formats for every file and entry
