# Rule: Every Pattern MUST Be Carried Out by at Least One Skill

Rule created: 2026-11-24T17:18:59-08:00
Rule modified: 2026-11-24T17:18:59-08:00

Status: Proposed

Confidence: Low

## Description

Every Pattern MUST list at least one skill that carries it out in its Procedure, and each listed skill MUST exist in `.praxis/factory/skills/` or `.claude/skills/`. A Pattern's text is general; a skill carries it out with specific steps for a situation, and a Pattern may list several skills for different situations.

## Protection

A Pattern says what is done in general; only a skill says how, step by step, with tracked confidence. A Pattern no skill carries out cannot be carried out the same way twice.

The Pattern template's Procedure is where the skills are listed, and `praxis-flow-plan` chooses among them for each step of a Plan.

## Violation

A Pattern whose Procedure names no skill; a listed skill that does not exist.

## Exceptions

None.

## Conditions for Revision

Patterns whose one skill only repeats them become common (then the Pattern may be folded into the skill), or a Pattern is allowed to wait for its first skill.

## Domain Alignment

Reinforcing:
- Rule: Praxis Records MUST Conform to Their Templates and Lifecycles

Ambiguous:
- none known

Contradictory:
- none known
