# Plan Lifecycle

This document defines the lifecycle stages for plans tracked in `.praxis/state/plans.md`.
A Plan is a list of Tasks to perform during Act

## Stages

- Defined
- Approved
- Rejected
- Completed

## Stage Flow

Defined -> [ Approved | Rejected ]
Approved -> Completed

## Stage 0: Defined

The Tasks for the Plan Actions are documented.

**Entry Paths:**
- Tasks created in Plan phase

**Exit Paths:**
Approved:
- Discern phase approves the Tasks
Rejected:
- Discern phase rejects the Tasks

## Stage 1: Approved

The task is recorded and awaiting execution. Dependencies must be satisfied before moving to In Progress.

**Entry Paths:**
- Tasks approved in Discern phase

**Exit Paths:**
Completed:
- Tasks performed in the Act phase

## Stage 2: Completed

All sub-tasks are finished. Document outcomes and any artifacts produced.

**Entry Paths:**
- Tasks performed in the Act phase

## Stage 3: Rejected

Tasks will not be performed.

**Entry Paths:**
- Tasks rejected in the Discern phase

