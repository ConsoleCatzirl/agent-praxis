# Praxis State

State related to the current iteration of the Praxis Flow itself.

## List of State Types

A list of state types in the order they are created:

- **Tasks**: What to do, decomposed from the user prompt.
- **Plans**: How to complete Tasks.
- **Predictions**: Expected outcomes for each Plan.
- **Outcomes**: Recorded outcomes after performing each Plan.
- **Analyses**: Comparisons of Predictions and Outcomes.

A Plan takes steps towards fulfilling one or more Tasks.
A Plan gets a Prediction.
An Approved (or Bypassed) Plan gets an Outcome.
A Plan with an Outcome gets an Analysis.
Plans can depend on other Plans.

## Complexity Levels

Tasks and Plans are categorized into one of these Complexity levels:

1. **Trivial**: Descriptions, explanations, Q&A, request for conversation.
2. **Regex**: Can be completed using globs, pcre, sed, or awk.
3. **Mechanical**: Compound statements; lists of commands; glue code.
4. **Structural**: Requires the use of data structures.
5. **Qualitative**: Requires qualitative assessment or judgement.

## List of Result Types

Outcome Analyses categorize Results into these types:

- **Helpful**: All expected outcomes ocurred; beneficial unexpected outcomes.
- **Accurate**: All expected outcomes occurred; no unexpected outcomes ocurred.
- **Inaccurate**: All expected outcomes occurred; detrimental unexpected outcomes ocurred.
- **Incomplete**: Some expected outcomes did not occur; no unexpected outcomes ocurred.
- **Harmful**: Unauthorized access to external systems; data loss or unintended file removal; other disaster.

## List of State Items

For each state type, a list of state items can be found at `.praxis/state/${type}.md`,
with links to more information for each at `.praxis/state/${type}/${task-or-plan-name}.md`,
which are created from `.praxis/templates/${type}-template.md`.

## State Item Lifecycles

Each state type has its own lifecycle defined at `.praxis/lifecycles/${type}-lifecycle.md`.

