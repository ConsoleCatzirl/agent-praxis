# Confidence Level Lifecycle

Confidence follows two separate lifecycles simultaneously:
* Promotion/Deletion
* Subject Tracking

## Level Promotion/Demotion Lifecycle

Base rules for changing confidence levels of a subject.

### Levels

- None
- Low
- Medium
- High
- Complete

### Level Flow

State-machine grammar for this lifecycle:

None -> Low
Low -> [ None | Medium ]
Medium -> [ None | Low | High ]
High -> [ Low | Medium | Complete ]
Complete -> [ Medium | High ]

### Level 0: None

Lack of any confidence. Do not trust. Do not use. May be harmful.

**Entry Paths:**
- Direct user statement
- Consistent harmful or detrimental outcomes

**Exit Paths:**
Low:
- Revise subject based on new evidence

### Level 1: Low

Low confidence. Low use count, or has produced unexpected detrimental or harmful outcomes.

**Entry Paths:**
- Subject newly created by the agent.
- Subject has resulted in detrimental or harmful outcomes

**Exit Paths:**
None:
- Repeated detrimental or harmful outcomes
- user request
Medium:
- beneficial unanticipated outcomes
- repeated use without detrimental or harmful outcomes
- user request

### Level 2: Medium

Medium confidence. Used successfully across multiple cycles without harmful outcomes. Occasional failures noted but pattern is reliable.

**Entry Paths:**
- Subject newly created by the user.
- Subject used repeatedly without harmful outcomes

**Exit Paths:**
None:
- Repeated harmful outcomes
- user request or direct statement
Low:
- Repeated detrimental outcomes
- user request or direct statement
High:
- repeated use without any detrimental or harmful outcomes
- user request or direct statement

### Level 3: High

High confidence. consistent correct results across many cycles without any harmful or detrimental outcomes. Suitable for use without extra verification.

**Entry Paths:**
- repeated use without any unanticipated outcomes
- User request or direct statement

**Exit Paths:**
Low:
- Any harmful outcomes
- user request or direct statement
Medium:
- Any detrimental outcomes
- user request or direct statement
Complete:
- Numerous uses without any unantipated outcomes

### Level 4: Complete

Complete Confidence. Exhaustively verified with no known failure modes. Behavior is fully predictable. Reserved for items with extensive, consistent track records. Fewer confidence updates required.

**Entry Paths:**
- numerous uses without any unanticipated outcomes

**Exit Paths:**
Medium:
- Any harmful outcomes
- user request or direct statement
High:
- Any unanticipated outcomes

## Subject Tracking Lifecycle

### Stages

- Identified
- Tracked
- Trusted
- Abandoned

### Stage Flow

State-machine grammar for this lifecycle:

Identified -> Tracked
Tracked -> [ Trusted | Abandoned ]
Trusted -> Tracked

### Stage 0: Identified

Subject of confidence is identified (e.g. new tool/skill/belief).

**Entry Paths:**
- pattern recognition
- user request direct user statement

**Exit Paths:**
Tracked:
- subject added to `.praxis/tracking/confidence.md` and `.praxis/tracking/confidence-details.md`.

### Stage 1: Tracked

Confidence level of subject is being tracked.

**Entry Paths:**
- subject added to `.praxis/tracking/confidence.md` and `.praxis/tracking/confidence-details.md`.

**Exit Paths:**
Trusted:
- subject has reached complete confidence
Abandoned:
- explicit user request

### Stage 2: Trusted

Subject has complete confidence. Less tracking required.

**Entry Paths:**
- subject has reached complete confidence

**Exit Paths:**
Tracked:
- conditions or context has changed significantly
- subject has changed confidence level
- explicit user request

### Stage 3: Abandoned

Confidence level is no longer tracked.

**Entry Paths:**
- direct user statement

**Exit Paths:**
- subject removed from  `.praxis/tracking/confidence.md` and `.praxis/tracking/confidence-details.md`, the removal is logged in `.praxis/logs/confidence-log.md`.
