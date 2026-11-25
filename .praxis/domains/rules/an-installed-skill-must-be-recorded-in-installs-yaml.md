# Rule: An Installed Skill MUST Be Recorded in installs.yaml

Rule created: 2026-11-24T17:18:59-08:00
Rule modified: 2026-11-24T17:18:59-08:00

Status: Proposed

Confidence: Low

## Description

A skill MUST be in exactly one of `.praxis/factory/skills/` and `.claude/skills/<name>/`, and `.praxis/factory/installs.yaml` MUST name it if and only if it is in `.claude/skills/<name>/`, at the path where it is. A skill moves between the two only as the install lifecycle (`.praxis/lifecycles/install-lifecycle.md`) gives, by a move that leaves nothing behind.

## Protection

The agent finds installed skills only in `.claude/skills/<name>/`, and the factory finds the rest in `.praxis/factory/skills/`; a copy in both places, or an install the record does not show, makes the two disagree about what the agent can use and which confidence applies.

`praxis-install-skill` carries out the move and the record together.

## Violation

A skill directory in both places; a skill in `.claude/skills/<name>/` that `installs.yaml` does not list; an entry in `installs.yaml` whose path does not exist; a skill moved before the install lifecycle gives the move.

## Exceptions

None.

## Conditions for Revision

The install lifecycle changes its thresholds or the places skills live.

## Domain Alignment

Reinforcing:
- Rule: Praxis Records MUST Conform to Their Templates and Lifecycles

Ambiguous:
- none known

Contradictory:
- none known
