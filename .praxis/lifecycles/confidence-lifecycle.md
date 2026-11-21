# Confidence Level Lifecycle

Base rules for changing confidence levels of a subject.

## Levels

- None
- Low
- Medium
- High
- Complete

## Level Flow

State-machine grammar for this lifecycle:

```
Low -> [ None | Medium ]
Medium -> [ None | Low | High ]
High -> [ Low | Medium | Complete ]
Complete -> [ Medium | High ]
```

## Level 0: None

Do not trust. Do not use. Considered harmful.

No confidence in benefit or usefulness; confidence in lack of benefit or usefulness
Correlation with multiple harmful outcomes.
Strong correlation with detrimental outcomes.
Heavily contradicted by other domain items.

**Entry Paths:**
- Direct user statement
- Consistent harmful or detrimental outcomes

**Exit Paths:**
Low:
- Revise subject based on new evidence

## Level 1: Low

Low confidence in benefit or usefulness.

May correlate with both accurate and detrimental outcomes.
May be directly contradicted by evidence.
May have numerous contradictiory domain items.
May have limited evidence.

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

## Level 2: Medium

New or refined items with minimal information.
Medium confidence in accurate or helpful outcomes.
May correlate with accurate outcomes, occassional detrimental outcomes.
Potential ambiguity or contradiction with other domain items.
No correlated harmful outcomes.

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

## Level 3: High

Suitable for use without extra verification.

Strong correlation with accurate outcomes.
Correlation with multiple helpful outcomes.
Low ambiguity with other domain items.

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
- Numerous uses without any unanticipated outcomes

## Level 4: Complete

Complete Confidence. Exhaustively verified with no known failure modes. Behavior is fully predictable. Reserved for items with extensive, consistent track records. Fewer confidence updates required.

Long track record of a strong correlation with accurate or helpful outcomes. 
No correlation with harmful outcomes.
Minimal correlation with detrimental outcomes.
Highly reinforced and reinforcing.
Minimal contradictory domain items.

**Entry Paths:**
- numerous uses without any unanticipated outcomes

**Exit Paths:**
Medium:
- Any harmful outcomes
- user request or direct statement
High:
- Any unanticipated outcomes

