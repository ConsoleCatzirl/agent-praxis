---
name:
description:
---


## Stage 1: Proposed
**Entry Paths:**
Low: [ New ]
Medium: [ New | Proposed ]

- pattern recognition during learn
- indirect user statement
- move to skill?
Medium:
- direct user statement, with uncertainty
- pattern recognition during introspection
- Item has been heavily revised

**Exit Paths:**
Asserted:
- Item is tightly coupled with at least 1 other Asserted domain items
- Item is tightly coupled with at least 2 other Established domain items
- Item supports a helpful outcome.
Abandoned:
- Item is shown to be harmful
- direct user statement



## Stage 2: Asserted
**Entry Paths:**
High:
- direct user statement
- Item is tightly coupled with at least 2 other Established domain items
- Item supports a helpful outcome.
Complete:
- direct user statement, with certainty

**Exit Paths:**
Questioned:
- The item is a repeated source of contradiction with other items.
- Item or its consequences are questioned by the user.
Abandoned:
- explicit user request

## Stage 3: Questioned
**Entry Paths:**
Low:
- Item or its consequences are questioned by the user.
- The item is a source of contradiction with other items.
Medium:
- The item is a source of ambiguity with other items.

**Exit Paths:**
Asserted:
- re-affirm item correctness, importance, and fitness
Proposed:
- revise item for correctness, importance, or fitness
Abandoned:
- explicit user request
- 3 or more unresolvable contradictions

## Stage 3: Abandoned
**Entry Paths:**
None:
- Explicit user request
- Item is shown to be harmful or detrimental
- Item is shown to be harmful
- 3 or more unresolvable contradictions

**Exit Paths:**
Cleared:
- Item deemed no longer useful for synthesis.



---



### Confidence: None

No confidence in benefit or usefulness; confidence in lack of benefit or usefulness.

**Entry Conditions:**
- Item is related to repeated harmful outcomes
- Item is related to frequent detrimental outcomes

**Exit Conditions:**
None:
- No exit

### Confidence: Low

Low confidence in benefit or usefulness. May be lack of sufficient evidence, or contradictory evidence, or contradictiory domain items.

**Entry Conditions:**
- Contradicts with evidence
- Contradicts with domain items

**Exit Conditions:**
None:
- Related to any harmful outcomes
- Related to frequent detrimental outcomes
- Additional contradictory domain items
Medium:
- Related to any helpful outcomes
- Related to frequent accurate outcomes
- Reinforces or is reinforced by 3+ domain items with medium+ confidence

### Confidence: Medium

### Confidence: High

### Confidence: Complete


