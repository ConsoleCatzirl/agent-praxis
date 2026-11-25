# Praxis

The directory structure of `.praxis/`, the base directory for everything related to the Praxis Flow. The same text is in the root `README.md`.

## Directory Structure

`.praxis/`: Base directory for everything related to Praxis Flow

`.praxis/flow.md`: The Praxis Flow overview

`.praxis/glossary.md`: Definitions for key Praxis Flow terms

`.praxis/domains/`: Domains of items (beliefs, environment, expectations, intentions, opinions, practices, principles, rules, values); Asserted items are enforced

`.praxis/factory/`: The Factory: agents, habits, hooks, patterns, scripts, skills, and tools, with their READMEs and lists

`.praxis/factory/skills/`: All skills, including the Flow skills (`praxis-flow-*`); an installed skill is moved to `.claude/skills/<name>/` and recorded in `.praxis/factory/installs.yaml`

`.praxis/lifecycles/`: State-machine grammars for each component

`.praxis/state/`: State tracking for each run through the Praxis Flow

`.praxis/templates/`: Templates for all aspects of the Praxis Flow

`.praxis/tracking/`: Confidence tables, Signals, and introspections (`introspections.md` and `introspections/`) for the quality of the domains, the factory, and the Praxis Flow itself
