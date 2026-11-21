---

---


---

---

## Stage 1: Unstable
**Entry Path:**
New:
- Initial creation
Stable:
- Product requires significant modification.
- Product causes a harmful outcome.
Retired:
- Product is brought back into use.

**Exit Paths:**
Stable:
- Confidence level reaches High+
- 

## Stage 2: Stable

**Entry Paths:**
High:
- product is consistently accurate or helpful
Complete:
- Extensive use at High confidence

**Exit Paths:**

## Stage 3: Retired
**Entry Paths:**
None:
- user request to abandon product
Unchanged:
- product is superceded or deprecated 

**Exit Paths:**
Unstable:
- user request to bring out of retirement
- need or use-case becomes relavent again
Cleared:
- Deemed no-longer-useful as a reference

---


## Summary Table

| Stage | Name | Location | Confidence | Gate |
|-------|------|----------|------------|------|
| 0 | Observation | `confidence.md` commands table | Low | Reaches Medium |
| 1 | Pattern Recognition | `introspect` analysis | Medium | User approves incubation |
| 2 | Incubation | `.praxis/skills/incubation/` | Low → High | Reaches High |
| 3 | Discernment Review | `discern` verdict | High | AGREE verdict |
| 4 | Certified | `.praxis/skills/` | Ongoing | — |

## Stage Flow

Observation -> Pattern Recognition
Pattern Recognition -> [ Incubation | Abandoned ]
Incubation -> Discernment Review
Discernment Review -> [ Incubation | Certified | Abandoned ]
Certified -> Abandoned

## Stage 0: Observation

A command, tool sequence, or task pattern is executed and recorded in `confidence.md`.

- The behavior is tracked in the Commands or Tools table.
- Confidence starts at Low.
- No skill exists yet — this is raw observed behavior.

**Entry trigger:** Any command run or tool used during a praxis cycle.
**Exit trigger:** Confidence reaches Medium through repeated correct use.

## Stage 1: Pattern Recognition

During `introspect` (step 6 — Commands Pattern Analysis), the agent reviews the commands table for:
- Commands that share a common structure (candidates for regex consolidation)
- Commands with Medium or higher confidence that represent a repeatable, nameable behavior

If a command or pattern looks like it could be a skill:
- Draft a name and purpose
- Assess whether it can be generalized with parameters
- Propose to user via `consent`

**Entry trigger:** Command reaches Medium confidence + introspect identifies skill candidacy.
**Exit trigger:** User approves incubation.

## Stage 2: Incubation

An approved skill candidate is drafted using `.praxis/templates/skill-incubation-template.md` and placed in `.praxis/skills/incubation/`.

The skill is added to the Skills table in `confidence.md` at Low confidence.

During this stage:
- The skill is used under supervision — the agent invokes it and reflects on outcomes
- Each use is recorded as confidence evidence.
- Supervision notes are added to the incubation file after each cycle
- Confidence is updated via the `learn` skill after each use

**Entry trigger:** User approves incubation; file created in `.praxis/skills/incubation/`.
**Exit trigger:** Skill confidence reaches High through supervised use.

## Stage 3: Discernment Review

Before promotion, `discern` is invoked to assess the incubating skill for integrity:

- Does the skill align with stated values?
- Does it protect needs (e.g. does it require consent where appropriate)?
- Is it safe to run without supervision?
- Are there any reversibility concerns?

A AGREE verdict is required to proceed to promotion.
A CONCERN is documented and may proceed if the concern is a known trade-off.
A BLOCK requires revision before promotion can be reconsidered.

**Entry trigger:** Skill confidence reaches High.
**Exit trigger:** Discern returns SOUND or CONCERN (documented).

## Stage 4: Promotion

The agent proposes promotion to the user via `consent`.

If approved:
- Move the skill file from `.praxis/skills/incubation/` to `.praxis/skills/`
- Update the skill file to use the certified skill template (`.praxis/templates/skill-template.md`)
- Update `confidence.md`: move the skill entry from incubating to the main Skills table, retaining its current confidence level
- Log the promotion in git.

**Entry trigger:** User approves promotion via consent.
**Exit trigger:** File moved, confidence updated, promotion logged in git.

## Stage 5: Certified Use

The skill is in `.praxis/skills/` and is invoked as part of normal praxis cycles.

- Confidence continues to be updated via `learn` after each use
- If the skill consistently underperforms, `introspect` may flag it for revision
- Major revisions return the skill to Stage 2 (Incubation) under a new supervision cycle

**Entry trigger:** Skill promoted through user approval (→ Promotion).
