# Install Lifecycle

## Stages

- Uninstalled
- Installed

## Stage Flow

State-machine grammar for this lifecycle:

```
New -> Uninstalled
Uninstalled -> [ Installed | Cleared ]
Installed -> Uninstalled
```

## Stage 1: Uninstalled

The product lives in `.praxis/factory/` and is run by its path. Installation is an axis of its own, recorded in `.praxis/factory/installs.yaml`, apart from its stage in the factory lifecycle. Products with no installed location (scripts, habits) stay Uninstalled.

**Entry Paths:**
Any: New
None: Installed
Any (the product Retired): Installed

**Exit Paths:**
Installed: [ High | Complete ] (a `praxis-flow-*` skill: [ Medium | High | Complete ]; an agent: [ Low | Medium | High | Complete ])
Cleared: Any (the product Cleared)

## Stage 2: Installed

The product's files live at its installed location, where Claude Code finds it (a skill in `.claude/skills/<name>/`; an agent in `.claude/agents/<name>.md`), moved out of `.praxis/factory/` with nothing left behind, and `.praxis/factory/installs.yaml` records where. It stays installed through any stage of the factory lifecycle, Unstable included, until its confidence is None or it is Retired (a fall from Low to None is itself a retirement, in the same move: `factory-lifecycle.md`): the threshold to install is higher than the one to uninstall, so a product does not go in and out as its confidence moves. A product that is Installed and Unstable is a priority for improving its confidence, and is a finding to report. Agents have a standing exception: an agent is installed from Low, since the Agent tool calls only installed agents and their use is the evidence for their confidence.

**Entry Paths:**
High: Uninstalled
Complete: Uninstalled
Medium: Uninstalled (a `praxis-flow-*` skill or an agent)
Low: Uninstalled (an agent only, a standing exception)

**Exit Paths:**
Uninstalled: [ None ], or Any when the product is Retired
