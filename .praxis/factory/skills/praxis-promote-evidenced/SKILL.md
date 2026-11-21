---


---



## Stage 1: Hypothesized
**Entry Paths:**

Low:
- First occurrence of an observation or inference that suggests a pattern or truth.

Medium:
- Direct user request or statement.
- Low-confidence item is confirmed once.

**Exit Paths:**

Evidenced:
- Sufficient evidence has been observed for a medium-confidence item, without any contradictory evidence observed.

Debunked:
- Item deemed unsupported.

## Stage 2: Evidenced
**Entry Paths:**

Medium:
- Observation of independent supporting evidence for a Hypothesized item.
- Challenged item (Medium confidence) is deemed correct with or without changes.

**Exit Paths:**

Established:
- Item consistently confirmed without contradiction.

Challenged:
- Contradicting evidence appears.

## Stage 3: Established
**Entry Paths:**

Medium:
- Evidenced item is shown to be consistently correct.

High:
- Challenged item (High confidence) is deemed correct without alteration.
- Established item (Complete confidence) is contradicted once.

Complete:
- Established item (High confidence) is shown to be resilient across a variety contexts.
- Established item (High confidence) is shown to be exceptionally consistent.

**Exit Paths:**

Challenged:
- Contradicting evidence appears for a high-confidence established item.
- Context and/or conditions change significantly.

## Stage 4: Challenged
**Entry Paths:**

Low:
- Counter-evidence is observed for Evidenced item.

Medium:
- Supporting evidence is observed for low-confidence challenged item after alteration.
- Counter-evidence is observed for medium-confidence Established item.
- `introspect` flags inconsistency.
- Direct user request or statement.

High:
- Counter-evidence is observed for high-confidence established item.

**Exit Paths:**

Evidenced:
- Item altered to resolve contradiction.

Established:
- Contradiction resolved with item upheld.

Debunked:
- item deemed unfounded.

## Stage 5: Debunked
**Entry Paths:**
- Item deemed unfounded.
- Direct user request or statement.

**Exit Paths:**
- The item is removed from `.praxis/domains/` and the change is committed to git.
