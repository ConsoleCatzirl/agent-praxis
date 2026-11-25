# Signal: Result Consistency

## Description

The share of Analyses whose Result agrees with their own Surprises and Unfulfilled lines by the definitions of `.praxis/state/README.md`.

## Metric

Consistent Analyses divided by all Analyses, per run and across runs: Accurate has no Surprise and nothing Unfulfilled; Helpful and Inaccurate have Surprises and nothing Unfulfilled; Incomplete has something Unfulfilled and no Surprise; Harmful is always consistent. Whether a Surprise was beneficial or detrimental is not checked.

## Purpose

Accurate Outcomes and Helpful Outcomes are only as good as the classification under them; this Signal shows when Analyses are classified loosely, or when no Result type fits.

## Notes

No values yet; `praxis-flow-learn` writes the first value under a Values heading when a run is recorded.
