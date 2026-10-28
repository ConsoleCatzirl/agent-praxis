# Pattern Lifecycle

This document defines the lifecycle stages for patterns tracked in `.praxis/tracking/patterns.md`.
Patterns are sets of tasks, tools, and/or skills that co-occur and composite.

## Stages

- Hypothesized
- Evidenced
- Established
- Challenged
- Abandoned

## Stage Flow

State-machine grammar for this lifecycle:

Hypothesized -> [ Evidenced | Abandoned ]
Evidenced -> [ Established | Challenged ]
Established -> Challenged
Challenged -> [ Evidenced | Established | Abandoned ]

## Stage 1: Hypothesized

A pattern is formed from a single observation or inference. It has not yet been confirmed by additional evidence.

**Confidence:** [ Low | Medium ]

**Entry Paths:**

Low:
- First occurrence of an observation that suggests a pattern or truth.

Medium:
- Low-confidence hypothesized pattern is repeated once.
- User request or direct statement

**Exit Paths:**

Evidenced:
- A third independent observation supports the pattern.

Abandoned:
- pattern deemed unsupported.

## Stage 2: Evidenced

The pattern is supported by 3 or more independent observations. It is plausible but not yet consistently confirmed.

**Confidence:** Medium

**Entry Paths:**

Medium:
- At least three supporting observations recorded

**Exit Paths:**

Established:
- Pattern consistently confirmed across many cycles

Abandoned:
- pattern deemed unsupported

## Stage 3: Established

The pattern has been confirmed repeatedly with no significant contradictions. It is treated as reliable for anticipation and decision-making.

**Confidence:** [ Medium | High ]

**Entry Paths:**

- High confidence reached through consistent confirmation.

**Exit Paths:**

Challenged:
- Contradicting evidence appears
- context and/or conditions change significantly

Abandoned:
- pattern deemed unsupported

## Stage 4: Challenged

Contradicting evidence has appeared. The pattern is under review — it may be revised, or the contradiction may be explained away.

**Confidence:** Medium

**Entry Paths:**

- An outcome contradicts the pattern
- `introspect` flags inconsistency
- conditions change significantly

**Exit Paths:**

Established:
- Contradiction resolved with pattern upheld
- pattern updated and verified

Abandoned:
-  pattern deemed unsupported

## Stage 5: Abandoned

The pattern has been discarded as no longer supported (Abandoned) based on new evidence.


**Entry Paths:**

- Pattern deemed unsupported at any stage.

**Exit Paths:**
- The pattern is removed from `.praxis/tracking/patterns.md`, and the change is committed to git.
