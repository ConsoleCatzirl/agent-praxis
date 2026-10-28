# Need Lifecycle

This document defines the lifecycle stages for needs held in `.praxis/steering/needs.md`.
Needs are non-negotiable requirements and constraints, they cannot be overridden by other each other or by any other domains.

Any change in lifecycle for a need requires explicit user approval.

## Stages

- Identified
- Established
- Questioned
- Abandoned

## Stage Flow

State-machine grammar for this lifecycle:

Identified -> Established
Established -> Questioned
Questioned -> [ Established | Abandoned ]

## Stage 0: Identified

Recognize a fundamental requirement or constraint that qualifies as a need.

**Entry Paths:**

- direct user statement
- repeated interaction and/or pattern recognition

**Exit Paths:**

Established:
- need documented in `.praxis/steering/needs.md` and `.praxis/steering/need-details.md`

## Stage 1: Established

The need is established and enforced. All actions must satisfy this need. Violations trigger immediate notification and remediation.

**Entry Paths:**

- need documented in `.praxis/steering/needs.md` and `.praxis/steering/need-details.md`

**Exit Paths:**

Questioned:
- The need is a repeated source of conflict within  or across steering domains.
- need or its consequences are questioned by the user.

Abandoned:
- explicit user request

## Stage 2: Questioned

The need is under review for correctness and fitness.
The need is a repeated source of conflict within  or across steering domains.

**Entry Paths:**
- The need is a repeated source of conflict within  or across steering domains.
- need or its consequences are questioned by the user.

**Exit Paths:**
Established:
- re-affirm need correctness and fitness
- revise need for correctness and/or fitness

Abandoned:
- explicit user request
- unresolvable conflict

## Stage 3: Abandoned

The need is permanently removed. This should be rare, as needs represent non-negotiable requirements.

**Entry Paths:**
- Explicit user request
- Identified as the source of an unresolvable conflict within or across steering domains

**Exit Paths:**
- The need is removed from `.praxis/steering/needs.md` and `.praxis/steering/need-details.md`, and the change is committed to git.
