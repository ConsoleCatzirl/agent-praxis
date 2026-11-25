# Rule: Praxis Records MUST Conform to Their Templates and Lifecycles

Rule created: 2026-11-24T17:18:59-08:00
Rule modified: 2026-11-24T17:18:59-08:00

Status: Proposed

Confidence: Low

## Description

Every file, item, and reference under `.praxis/` MUST conform to its template and lifecycle: lists match their directories, tracking rows match their items, statuses are valid lifecycle stages, each skill's name matches its directory, and references name files and items that exist.

## Protection

The soundness of the records that the flow reads and writes.

Skills and lifecycles act on records that are malformed or inconsistent, and the agent's picture of itself degrades. It is the rule the other structural Rules of this branch rest on.

`praxis-flow-learn` reviews Analyses for consistency before changes are recorded, and a structural check of the tree (links and references that resolve, statuses that are lifecycle stages) is the way to see a violation.

## Violation

A list entry with no details entry (or the reverse); a status that is not a stage of the entry's lifecycle; a reference to a file or entry that does not exist; a file that departs from its template without a recorded reason.

## Exceptions

- A departure from a template or lifecycle MAY stand when it is documented as a violation, until it is corrected.

## Conditions for Revision

A template or lifecycle changes in a way that makes the standard impossible to apply as written.

## Domain Alignment

Reinforcing:
- Rule: Every Habit Step MUST Name a Factory Product Other Than a Skill or Agent
- Rule: Every Pattern MUST Be Carried Out by at Least One Skill
- Rule: An Installed Skill MUST Be Recorded in installs.yaml

Ambiguous:
- none known

Contradictory:
- none known
