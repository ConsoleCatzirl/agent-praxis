# Practice Lifecycle

This document defines the lifecycle stages for practices held in `.praxis/guiding/practices.md`.
Practices define what the agent can reasonably anticipate from itself and interactions.

## Stages

- Identified
- Established
- Questioned
- Abandoned

## Stage Flow

State-machine grammar for this lifecycle:

Identified -> Established
Established -> [ Questioned | Abandoned ]
Questioned -> [ Established | Abandoned ]

## Stage 0: Identified

Recognize an practice that should be documented.

**Entry Paths:**
- direct user statement
- repeated interaction and/or pattern recognition

**Exit Paths:**
Established:
- practice documented in `.praxis/guiding/practices.md` and `.praxis/guiding/practices-details.md`

## Stage 1: Established

The practice is in force and is being tracked.

**Entry Paths:**
- practice documented in `.praxis/guiding/practices.md` and `.praxis/guiding/practices-details.md`

**Exit Paths:**
Questioned:
- The practice is a repeated source of conflict with other needs, principles, values, beliefs, opinions, or practices
- evidence conflicting with the practice is observed.
- practice or its consequences are questioned by the user.

Abandoned:
- explicit user request

## Stage 2: Questioned

The practice is under review for correctness and fitness.

**Entry Paths:**
- The practice is a repeated source of conflict with other needs, principles, values, beliefs, opinions, or practices
- evidence conflicting with the practice is observed.
- practice or its consequences are questioned by the user.

**Exit Paths:**
Established:
- re-affirm correctness and fitness
- revise practice for correctness and/or fitness

Abandoned:
- explicit user request

## Stage 3: Abandoned

The practice is permanently removed. This should be rare.

**Entry Paths:**
- Explicit user request
- unresolvable conflict with needs, values, or principles, requires user approval

**Exit Paths:**
- practice removed from `practices.md` and `details/practices-details.md`, and the change is committed to git.
