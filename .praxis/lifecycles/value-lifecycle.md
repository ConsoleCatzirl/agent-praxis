# Value Lifecycle

This document defines the lifecycle stages for values held in `.praxis/steering/beliefs.md`.
Values are core priorities that govern decision-making when trade-offs arise.
Priority between competing values are determined on a case-by-case basis.

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

A fundamental guiding priority that qualifies as a value has been recognized.

**Entry Paths:**
- direct user statement
- repeated interaction and/or pattern recognition
- Introspection pattern recognition

**Exit Paths:**
Established:
- value documented in `value.md` and `details/value-details.md`

## Stage 1: Established

The value is established and enforced. Violations trigger immediate notification and remediation.

**Entry Paths:**
- value documented in `value.md` and `details/value-details.md`

**Exit Paths:**
Questioned:
- The value is a repeated source of conflict with other needs, principles, values, goals, beliefs, or expectations
- value or its consequences are questioned by the user.

Abandoned:
- explicit user request

## Stage 2: Questioned

The value is under review for correctness and fitness.
The value is a repeated source of conflict with other needs, principles, values, goals, beliefs, or expectations.

**Entry Paths:**
- The value is a repeated source of conflict with other needs, principles, values, goals, beliefs, or expectations
- value or its consequences are questioned by the user.

**Exit Paths:**
Established:
- re-affirm value correctness and fitness
- revise value for correctness and/or fitness

Abandoned:
- explicit user request
- unresolvable conflict with needs, values, or principles

## Stage 3: Abandoned

The value is permanently removed. This should be rare, as values represent guiding priorities.

**Entry Paths:**
- Explicit user request
- unresolvable conflict with needs, values, or principles
