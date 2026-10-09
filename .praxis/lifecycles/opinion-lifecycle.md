# Opinion Lifecycle

This document defines the lifecycle stages for opinions held in `.praxis/guiding/opinions.md`.
Every opinion progresses through stages based on the evidence supporting it.

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

A opinion is formed from observation or inference. It has not yet been confirmed by additional evidence. The opinion may need heavy revision.

**Confidence:** [ Low | Medium ]

**Entry Paths:**

Low:
- First occurrence of an observation or inference that suggests a pattern or truth.

Medium:
- Direct user request or statement.
- Low-confidence opinion is confirmed once.

**Exit Paths:**

Evidenced:
- Sufficient evidence has been observed for a medium-confidence opinion, without any contradictory evidence observed.

Abandoned:
- Opinion deemed unsupported.

## Stage 2: Evidenced

The opinion is supported by multiple independent observations. It is plausible but not yet consistently confirmed. The opinion may need refinement, or may be under review after refinement.

**Confidence:** Medium

**Entry Paths:**

Medium:
- Observation of independent supporting evidence for a Hypothesized opinion.
- Challenged opinion (Medium confidence) is deemed correct with or without changes.

**Exit Paths:**

Established:
- Opinion consistently confirmed without contradiction.

Challenged:
- Contradicting evidence appears.

## Stage 3: Established

The opinion has been confirmed repeatedly with no significant contradictions. It is treated as reliable for anticipation and decision-making.

**Confidence:** [ Medium | High | Complete ]

**Entry Paths:**

Medium:
- Evidenced opinion is shown to be consistently correct.

High:
- Challenged opinion (High confidence) is deemed correct without alteration.
- Established opinion (Complete confidence) is contradicted once.

Complete:
- Established opinion (High confidence) is shown to be resilient across a variety contexts.
- Established opinion (High confidence) is shown to be exceptionally consistent.

**Exit Paths:**

Challenged:
- Contradicting evidence appears for a high-confidence established opinion.
- Context and/or conditions change significantly.

## Stage 4: Challenged

Contradicting evidence has appeared. The opinion is under review — it may be revised, or the contradiction may be explained away.

**Confidence:** [ Low | Medium | High ]

**Entry Paths:**

Low:
- Counter-evidence is observed for Evidenced opinion.

Medium:
- Supporting evidence is observed for low-confidence challenged opinion after alteration.
- Counter-evidence is observed for medium-confidence Established opinion.
- `introspect` flags inconsistency.
- Direct user request or statement.

High:
- Counter-evidence is observed for high-confidence established opinion.

**Exit Paths:**

Evidenced:
- Opinion altered to resolve contradiction.

Established:
- Contradiction resolved with opinion upheld.

Abandoned:
- opinion deemed unfounded.

## Stage 5: Abandoned

The opinion has been discarded as no longer supported (Abandoned) based on new evidence or user request.

The opinion is removed from `.praxis/guiding/opinions.md`. The removal is logged in `.praxis/logs/opinion-log.md`.

**Confidence:** None

**Entry Paths:**
- Opinion deemed unfounded.
- Direct user request or statement.
