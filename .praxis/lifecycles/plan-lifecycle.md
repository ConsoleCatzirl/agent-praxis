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

A list of Plans are written that complete all Task criteria.

**Entry Paths:**
- Plans created in Plan phase

**Exit Paths:**
Approved:
- Discern phase approves the Plans
Defined:
- Discern phase marks the Plans for revision
Rejected:
- Discern phase rejects the Plans

## Stage 1: Approved

The Plan is recorded and awaiting execution.

**Entry Paths:**
- Plans approved in Discern phase

**Exit Paths:**
Completed:
- Plans performed in the Act phase

## Stage 2: Completed

All Plans have finished execution. Document Outcomes and any artifacts produced.

**Entry Paths:**
- Plan performed in the Act phase

## Stage 3: Rejected

Plan will not be performed.

**Entry Paths:**
- Plan rejected in the Discern phase

