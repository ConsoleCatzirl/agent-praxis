# Principle Lifecycle

This document defines the lifecycle stages for principles held in `.praxis/steering/principles.md`.
These are the core principles for conduct in this project. They govern how this agent thinks, acts, and learns — in every context, without exception.

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

A principle is identified or proposed.

**Entry Paths:**
- direct user statement
- repeated interaction and/or pattern recognition

**Exit Paths:**
Established:
- principle documented in `.praxis/steering/principles.md` and `.praxis/steering/principle-details.md`

## Stage 1: Established

The principle is in force and is being tracked.
The principle governs thinking, acting, learning, and responding. Violations should be caught during reflection and corrected.

**Entry Paths:**
- principle documented in `.praxis/steering/principles.md` and `.praxis/steering/principle-details.md`

**Exit Paths:**
Questioned:
- The principle is a repeated source of conflict with other needs, principles, values.
- principle or its consequences are questioned by the user.

Abandoned:
- explicit user request

## Stage 2: Questioned

The principle is a repeated source of conflict in decision-making or behavior guidance. It requires evaluation to determine if the principle is correctly formulated or if it should be reclassified.

**Entry Paths:**
- The principle is a repeated source of conflict with other needs, principles, values. 
- principle or its consequences are questioned by the user.

**Exit Paths:**
Established:
- re-affirm correctness and fitness
- revise principle for correctness and/or fitness

Abandoned:
- explicit user request

## Stage 3: Abandoned

The principle has been removed from active consideration. Evidence of the principle remains in git logs.

**Exit Paths:**
- Principle is removed from `.praxis/steering/principles.md` and `.praxis/steering/principle-details.md`, removal is committed to git.
