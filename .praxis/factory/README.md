# Praxis Factory

Create scripts, skills, hooks, tools, agents, and patterns to connect them; track their confidence; create trusted automation.

## List of Factory Product Types

- **Agent**: Custom agent definitions.
- **Habits**: Repeatable sequences of scripts, hooks, tools or other habits.
- **Hooks**: Custom hook definitions.
- **Patterns**: Pattern definitions, connecting other products together.
- **Scripts**: Custom script definitions.
- **Skills**: Custom skill definitions.
- **Tools**: Custom tool definitions.

## List of Factory Products

A list of each product can be found in `.praxis/factory/${type}.md`, and what is installed in `.praxis/factory/installs.yaml`.

## Factory Product Lifecycles

All factory product types use the factory lifecycle at `.praxis/lifecycles/factory-lifecycle.md`.

## Factory Products and Complexity Levels

Factory products should be right-sized to their complexity levels.

**Regex**:
For anything larger than simple substitutions, prioritize `sed` scripts calling `.sed` files, combined with `grep -E`, `find`, `head`, `tail`, `cut`, `sort`, and `tr` (not an exhaustive list). Python can use `pythonsed` for consuming `.sed` files. Perl or Raku can be used with extreme caution for complex cases (beware the potential of ambiguous statements in the grammar).

**Mechanical**:
Shell scripts with compound conditional statements, process substition, and process redirection can be powerful.
Alternatively, Python scripts and/or libraries can easily be consumed by structural Python scripts.

**Structural**:
Prioritize Python for scripts that require data structures. Use `numpy` and/or `pandas` for advanced cases.

**Qualitative**:
Create a skill when qualitative assessment is required.
