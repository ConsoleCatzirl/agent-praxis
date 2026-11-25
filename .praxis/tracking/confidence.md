# Confidence Tracking

## Confidence Tables

### Evidence-Based Domain Items

[Beliefs](./confidence/beliefs.csv)
Columns: `confidence`, `lifecycle`, `details`, `name`
`confidence`: confidence level for this belief.
`lifecycle`: lifecycle state for this belief.
`details`: file name with details for this belief.
`name`: the name of this belief.

[Expectations](./confidence/expectations.csv)
Columns: `confidence`, `lifecycle`, `details`, `name`
`confidence`: confidence level for this expectation.
`lifecycle`: lifecycle state for this expectation.
`details`: file name with details for this expectation.
`name`: the name of this expectation.

[Patterns](./confidence/patterns.csv)
Columns: `confidence`, `lifecycle`, `complexity`, `details`, `name`
`confidence`: confidence level for this pattern.
`lifecycle`: lifecycle state for this pattern.
`complexity`: highest complexity level of any factory product used by this pattern
`details`: file name with details for this pattern.
`name`: the name of this belief.

### Factory Products

[Scripts](./confidence/scripts.csv)
Columns: `script`, `confidence`, `lifecycle`, `run-count`
`script`: the factory script being tracked
`confidence`: the confidence level for this script
`lifecycle`: the lifecycle state for this script
`run-count`: run count since last modification

[Skills](./confidence/skills.csv)
Columns: `skill`, `model`, `effort`, `complexity`, `confidence`, `lifecycle`, `run-count`
`skill`: the factory skill being tracked
`model`: the model for this confidence level and run count
`effort`: the effort level for this confidence level and run count
`complexity`: highest complexity level of this skill
`confidence`: the confidence level for this skill
`lifecycle`: lifecycle state for this skill.
`run-count`: run count for this skill at this confidence level

[Agents](./confidence/agents.csv)
Columns: `agent`, `model`, `effort`, `confidence`, `lifecycle`, `run-count`
`agent`: the factory agent being tracked
`model`: the model for this confidence level and run count
`effort`: the effort level for this confidence level and run count
`confidence`: the confidence level for this agent
`lifecycle`: lifecycle state for this agent.
`run-count`: run count for this agent at this confidence level

[Habits](./confidence/habits.csv)
Columns: `habit`, `confidence`, `lifecycle`, `run-count`
`habit`: the factory habit being tracked
`confidence`: the confidence level for this habit
`lifecycle`: lifecycle state for this habit.
`run-count`: run count for this habit at this confidence level

[Hooks](./confidence/hooks.csv)
Columns: `hook`, `confidence`, `lifecycle`, `run-count`
`hook`: the factory skill being tracked
`confidence`: the confidence level for this hook
`lifecycle`: lifecycle state for this hook.
`run-count`: run count for this hook at this confidence level

[Tools](./confidence/tools.csv)
Columns: `tool`, `confidence`, `lifecycle`, `run-count`
`tool`: the factory skill being tracked
`confidence`: the confidence level for this tool
`lifecycle`: lifecycle state for this tool.
`run-count`: run count for this tool at this confidence level

### Praxis Stage Delegation

[praxis-stage-models](./confidence/praxis-stage-models.csv)
Purpose: Track confidence of each model+effort for each stage+complexity for agent delegation.
Columns: `model`, `effort`, `stage`, `complexity`, `confidence`, `run-count`
`model`: the module used for delegation
`effort`: the effort level used for delegation
`stage`: the stage being delegated
`complexity`: the complexity of the plan processed by delegation
`confidence`: confidence level that this combo will be correct on the first pass
`run-count`: run count for this combo at this confidence level
