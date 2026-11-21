# Evidence-Based Lifecycle

This document defines the lifecycle stages for evidenced-based items held in `.praxis/domains/`.
Every item progresses through stages based on the evidence supporting and/or contradicting it.


## Stages

- Hypothesized
- Evidenced
- Established
- Challenged
- Debunked

### Stage Flow

State-machine grammar for this lifecycle:

```
New -> Hypothesized
Hypothesized -> [ Evidenced | Debunked ]
Evidenced -> [ Established | Challenged ]
Established -> Challenged
Challenged -> [ Evidenced | Established | Debunked ]
Debunked -> Cleared
```

### Stage 1: Hypothesized

An item is formed from observation or inference. It has not yet been confirmed by additional evidence. The item may need heavy revision.

**Confidence:** [ Low | Medium ]

**Entry Paths:**
Low: [ New ]
Medium: [ New | Hypothesized ] 

**Exit Paths:**
Hypothesized: [ Low | Medium ]
Evidenced: [ Medium ]
Debunked: [ None ]

### Stage 2: Evidenced

The item is supported by multiple independent observations. It is plausible but not yet consistently confirmed. The item may need refinement, or may be under review after refinement.

**Confidence:** [ Medium | High ]

**Entry Paths:**
Medium: [ Hypothesized | Challenged ]
High: [ Evidenced | Challenged ]

**Exit Paths:**
Evidenced: [ Medium | High ]
Established: [ Medium | High ]
Challenged: [ Low | Medium ]

### Stage 3: Established

The item has been confirmed repeatedly with no significant contradictions. It is treated as reliable for anticipation and decision-making.

**Confidence:** [ Medium | High | Complete ]

**Entry Paths:**
Medium: [ Evidenced | Established | Challenged ]
High: [ Evidenced | Established ] 
Complete: Established

**Exit Paths:**
Established: [ Medium | High | Complete ]
Challenged: [ Medium | High ]

### Stage 4: Challenged

Contradicting evidence has appeared. The item is under review — it may be revised, or the contradiction may be explained away.

**Confidence:** [ Low | Medium ]

**Entry Paths:**
Low: [ Evidenced | Challenged ]
Medium: [ Evidenced | Established | Challenged ]

**Exit Paths:**
Evidenced: [ Medium | High ]
Established: [ Medium ]
Debunked: [ None ]

### Stage 5: Debunked

The item has been discarded as no longer supported (abandoned) based on new evidence or user request.

**Confidence:** [ None ]

**Entry Paths:**
None: [ Hypothesized | Challenged ]

**Exit Paths:**
Challenged: [ Low ]
Cleared: [ None ]
