# Rules

## Rule Lifecycle

Rules follow the assertion-based lifecycle defined at `.praxis/lifecycles/assertion-lifecycle.md`.

## Rule Template

Each rule is created at `.praxis/domains/rules/${item-name}.md` from `.praxis/templates/rule-template.md`.

A rule's name has the form `X V Y`, where V is MUST or SHOULD in capitals, with NOT after it for the negation (MUST NOT, SHOULD NOT): "Every Prompt MUST Follow the Flow". X names the thing governed and Y a predicate that can be checked. The Description states the same requirement in full. Items that express one idea at a different commitment share a stem (`.praxis/domains/README.md`, "Naming").

## List of Rules

A list of rules can be found at `.praxis/domains/rules.md`, with links to more information for each at `.praxis/domains/rules/${item-name}.md`.
