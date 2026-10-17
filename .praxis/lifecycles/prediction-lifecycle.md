# Prediction Lifecycle

This document defines the lifecycle stages for plans tracked in `.praxis/state/predictions.md`.
Predictions are anticipations of task outcomes made during the Anticipate phase.

## Stages

- Created
- Rejected
- Approved
- Actualized
- Analyzed

## Stage Flow

State-machine grammar for this lifecycle:

Created -> [ Rejected | Approved ]
Approved -> Actualized
Actualized -> Analyzed
[ Rejected | Analyzed ] -> Cleared

## Stage 1: Created

Anticipated outcomes are documented in memory/predictions.md

**Entry Paths:**
- Document anticipated outcomes for a given Plan

**Exit Paths:**
Approved:
- Plan is Approved for performing
Rejected:
- Plan is marked Rejected

## Stage 2: Rejected

The Plan must not be performed.

**Entry Paths:**
- Plan is deemed unacceptable or inappropriate

**Exit Paths:**
Cleared:
- Plan is cleared from state/plans.md

## Stage 2: Actualized

Actualized outcomes are documented in memory/predictions.md

**Entry Paths:**
- Tasks performed

**Exit Paths:**
- Prediction analysis performed

## Stage 3: Rejected

Anticipated outcomes are detrimental or harmful. No actualized outcomes.

**Entry Paths:**
- Tasks rejected

**Exit Paths:**
- Prediction analysis performed

## Stage 3: Analyzed

Anticipated and Actualized outcomes (or rejection reason) have been compared and learnings have been documented.

**Entry Paths:**
- Tasks performed
- Tasks rejected

**Exit Paths:**
- Outcome analysis is completed and relavent praxis documents are updated.
