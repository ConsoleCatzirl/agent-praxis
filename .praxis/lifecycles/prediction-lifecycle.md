# Prediction Lifecycle

This document defines the lifecycle stages for plans tracked in `.praxis/state/predictions.md`.
Predictions are anticipations of task outcomes made during the Anticipate phase.

## Stages

- Created
- Actualized
- Rejected
- Analyzed

## Stage Flow

State-machine grammar for this lifecycle:

Created -> [ Actualized | Rejected ]
[ Actualized | Rejected ] -> Analyzed

## Stage 1: Created

Anticipated outcomes are documented in memory/predictions.md

**Entry Paths:**
- begin new prediction

**Exit Paths:**
Actualized:
- Tasks are performed
Rejected:
- Tasks are rejected

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
