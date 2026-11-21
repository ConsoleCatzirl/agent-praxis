# Factory Lifecycle

## Stages

- Unstable
- Stable
- Retired

### Stage Flow

State-machine grammar for this lifecycle:

```
New -> Unstable
Unstable -> [ Stable | Retired | Cleared ]
Stable -> [ Unstable | Retired ]
Retired -> [ Unstable | Cleared ]
```

### Stage 1: Unstable

**Confidence:** [ Low | Medium ]

**Entry Path:**
Low: [ New | Retired ]
Medium: [ New | Stable | Retired ]

**Exit Paths:**
Unstable: [ Low | Medium ]
Stable: High
Retired: [ None | Low | Medium ]
Cleared: None

### Stage 2: Stable

**Confidence:** [ High | Complete ]

**Entry Paths:**
High: [ Unstable | Stable ]
Complete: Stable

**Exit Paths:**
Stable: [ High | Complete ]
Retired: [ High | Complete ]
Unstable: [ Medium ]

### Stage 3: Retired

**Confidence:** [ Any ]

**Entry Paths:**
None: Unstable
Low: Unstable
Medium: Unstable
High: Stable
Complete: Stable

**Exit Paths:**
Unstable: [ None | Low | Medium ]
Stable: [ High | Complete ]

