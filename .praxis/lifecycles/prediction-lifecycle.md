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
[ Rejected | Actualized ] -> Analyzed

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

Anticipated Outcomes are detrimental or harmful. No Actualized Outcomes.
The Plan must not be performed.

**Entry Paths:**
- Plan is deemed unacceptable or inappropriate

**Exit Paths:**
Analyzed:
- Prediction analysis performed

## Stage 3: Approved

This Prediction's Plan is approved and ready to be performed.

**Entry Paths:**
- Discern approves Prediction and its Plan

**Exit Paths:**
Actualized:
- The plan is performed in `praxis-act`

## Stage 4: Actualized

Actualized outcomes are documented in memory/predictions.md

**Entry Paths:**
- Tasks performed

**Exit Paths:**
- Prediction analysis performed

## Stage 5: Analyzed

Anticipated and Actualized outcomes (or rejection reason) have been compared and learnings have been documented.

**Entry Paths:**
- Plans performed
- Plans rejected

**Exit Paths:**
- Outcome analysis is completed and relevant praxis documents are updated.
