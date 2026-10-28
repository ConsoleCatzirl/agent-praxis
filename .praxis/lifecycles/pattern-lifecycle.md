# Pattern Lifecycle

This document defines the lifecycle stages for patterns tracked in `.praxis/tracking/patterns.md`.
Patterns are sets of tasks, tools, and/or skills that co-occur and composite.

## Stages

- Identified
- Established
- Questioned
- Abandoned

## Stage Flow

State-machine grammar for this lifecycle:

Identified -> [ Established | Questioned ]
Established -> Questioned
Questioned -> [ Established | Abandoned ]

## Stage 1: Identified

A pattern is formed from a single observation or inference. It has not yet been confirmed by additional evidence.

**Confidence:** [ Low | Medium ]

**Entry Paths:**

Low:
- First occurrence of or need for a given Pattern.

Medium:
- Low-confidence identified pattern is repeated once.
- User request or direct statement

**Exit Paths:**

Evidenced:
- A third use of the pattern.

Abandoned:
- pattern deemed unsupported.

## Stage 2: Established

The pattern is supported by 3 or more independent uses.

**Confidence:** [ Medium | High | Complete ]

**Entry Paths:**

Medium:
- At least three supporting observations recorded

High:
- Numerous supporting observations

Complete:
- Even more numerous supporting observations

**Exit Paths:**

Questioned:
- pattern is contradictory or inconsistent
- context and/or conditions change significantly

## Stage 3: Questioned

Contradicting evidence has appeared. The pattern is under review — it may be revised, or the contradiction may be explained away.

**Confidence:** [ Low | Medium | High ]

**Entry Paths:**

Low:
- Contradicting evidence appears for a subject with Medium confidence

Medium:
- Contradicting evidence appears for a subject with High confidence

High:
- Contradicting evidence appears for a subject with Complete confidence

**Exit Paths:**

Established:
- Contradictions and inconsistencies are resolved

Abandoned:
- Contradicting evidence appears for a subject with Low confidence

## Stage 5: Abandoned

The pattern has been discarded as no longer supported.

**Entry Paths:**
- Pattern deemed unsupported or harmful

**Exit Paths:**
- The pattern is removed from `.praxis/tracking/patterns.md`, and the change is committed to git.
