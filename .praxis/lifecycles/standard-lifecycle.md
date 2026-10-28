# Standard Lifecycle

This document defines the lifecycle stages for standards held in `.praxis/steering/standards.md`.
Standards define a compass for making decisions, guiding the way to ideal outcomes.

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

Recognize an standard that should be documented.

**Entry Paths:**
- direct user statement
- repeated interaction and/or pattern recognition

**Exit Paths:**
Established:
- standard documented in `.praxis/steering/standards.md` and `.praxis/steering/standard-details.md`

## Stage 1: Established

The standard is active and is being tracked.

**Entry Paths:**
- standard documented in `.praxis/steering/standards.md` and `.praxis/steering/standard-details.md`

**Exit Paths:**
Questioned:
- The standard is a repeated source of conflict with other needs, principles, values, beliefs, standards, or expectations
- evidence conflicting with the standard is observed.
- standard or its consequences are questioned by the user.

Abandoned:
- explicit user request

## Stage 2: Questioned

The standard is under review for correctness or fitness.

**Entry Paths:**
- The standard is a repeated source of conflict with other needs, principles, values, standards, beliefs, or expectations
- evidence conflicting with the standard is observed.
- standard or its consequences are questioned by the user.

**Exit Paths:**
Established:
- re-affirm correctness and fitness
- revise standard for correctness and/or fitness and verify correctness/fitness

Abandoned:
- unresolvable conflict with needs, values, or principles
- explicit user request

## Stage 3: Abandoned

The standard is permanently removed. This should be rare.

**Entry Paths:**
- Explicit user request

**Exit Paths:**
- The standard is removed from `standards.md` and `standard-details.md`, removal is logged in git.
