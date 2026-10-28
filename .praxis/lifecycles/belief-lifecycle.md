# Belief Lifecycle

This document defines the lifecycle stages for beliefs held in `.praxis/guiding/beliefs.md`.
Every belief progresses through stages based on the evidence supporting and/or contradicting it.

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

A belief is formed from observation or inference. It has not yet been confirmed by additional evidence. The belief may need heavy revision.

**Confidence:** [ Low | Medium ]

**Entry Paths:**

Low:
- First occurrence of an observation or inference that suggests a pattern or truth.

Medium:
- Direct user request or statement.
- Low-confidence belief is confirmed once.

**Exit Paths:**

Evidenced:
- Sufficient evidence has been observed for a medium-confidence belief, without any contradictory evidence observed.

Abandoned:
- Belief deemed unsupported.

## Stage 2: Evidenced

The belief is supported by multiple independent observations. It is plausible but not yet consistently confirmed. The belief may need refinement, or may be under review after refinement.

**Confidence:** Medium

**Entry Paths:**

Medium:
- Observation of independent supporting evidence for a Hypothesized belief.
- Challenged belief (Medium confidence) is deemed correct with or without changes.

**Exit Paths:**

Established:
- Belief consistently confirmed without contradiction.

Challenged:
- Contradicting evidence appears.

## Stage 3: Established

The belief has been confirmed repeatedly with no significant contradictions. It is treated as reliable for anticipation and decision-making.

**Confidence:** [ Medium | High | Complete ]

**Entry Paths:**

Medium:
- Evidenced belief is shown to be consistently correct.

High:
- Challenged belief (High confidence) is deemed correct without alteration.
- Established belief (Complete confidence) is contradicted once.

Complete:
- Established belief (High confidence) is shown to be resilient across a variety contexts.
- Established belief (High confidence) is shown to be exceptionally consistent.

**Exit Paths:**

Challenged:
- Contradicting evidence appears for a high-confidence established belief.
- Context and/or conditions change significantly.

## Stage 4: Challenged

Contradicting evidence has appeared. The belief is under review — it may be revised, or the contradiction may be explained away.

**Confidence:** [ Low | Medium | High ]

**Entry Paths:**

Low:
- Counter-evidence is observed for Evidenced belief.

Medium:
- Supporting evidence is observed for low-confidence challenged belief after alteration.
- Counter-evidence is observed for medium-confidence Established belief.
- `introspect` flags inconsistency.
- Direct user request or statement.

High:
- Counter-evidence is observed for high-confidence established belief.

**Exit Paths:**

Evidenced:
- Belief altered to resolve contradiction.

Established:
- Contradiction resolved with belief upheld.

Abandoned:
- belief deemed unfounded.

## Stage 5: Abandoned

The belief has been discarded as no longer supported (abandoned) based on new evidence or user request.

**Confidence:** None

**Entry Paths:**
- Belief deemed unfounded.
- Direct user request or statement.

**Exit Paths:**
- The belief is removed from `.praxis/guiding/beliefs.md` and the change is committed to git.
