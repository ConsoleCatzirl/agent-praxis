# Assertion-Based Lifecycle

This document defines the assertion-based lifecycle stages.

## Stages

- Proposed
- Asserted
- Questioned
- Abandoned

### Stage Flow

State-machine grammar for this lifecycle:

```
New -> [ Proposed | Asserted ]
Proposed -> [ Asserted | Abandoned ]
Asserted -> [ Questioned | Abandoned ]
Questioned -> [ Asserted | Proposed | Abandoned ]
Abandoned -> Cleared
```

### Stage 1: Proposed

An item has been identified, but it's importance or validity is in question.
The item is informative, but not required.

**Confidence:** [ Low | Medium ]

**Entry Paths:**
* Low: New
* Medium: [ New | Proposed ]

**Exit Paths:**
* Proposed: [ Low | Medium ]
* Asserted: High
* Abandoned: None

### Stage 2: Asserted

The item is asserted and enforced.
Violations trigger immediate notification and remediation.
Exceptions required documented rationale.

**Confidence:** [ High | Complete ]

**Entry Paths:**
High: [ Asserted | Proposed ]
Complete: Asserted

**Exit Paths:**
Asserted: [ High | Complete ]
Questioned: [ Medium ]
Abandoned: [ None ]

### Stage 3: Questioned

The item is under review for correctness, importance, and fitness.
The item is informative, but not enforced.

**Confidence:** [ Low | Medium ]

**Entry Paths:**
Low: [ Asserted | Questioned ]
Medium: [ Asserted | Questioned ]

**Exit Paths:**
Asserted: High
Proposed: [ Low | Medium ]
Abandoned: None

### Stage 4: Abandoned

The item is deemed incorrect, unimportant, or unfit, with stated rationale.
The item or it's rationale remains useful for arbitrary synthesis.

**Confidence:** None

**Entry Paths:**
None: [ Proposed | Asserted | Questioned ]

**Exit Paths:**
Cleared: None

