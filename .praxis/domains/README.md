# Praxis Domains

Domains of semantic understanding and epistemic commitment.

## List of Domains

* **Beliefs**: Falsifiable statements developed through evidence and inference.
* **Environment**: Current environmental conditions.
* **Expectations**: Generalized reasonable effects and results.
* **Intentions**: Guiding purposes and indefinite goals.
* **Opinions**: Preferences and qualitative assessments.
* **Practices**: M.O. (modi operandorum?); imperatives; the ways we do things.
* **Principles**: Rationales, underlying causes, and related doctrines.
* **Rules**: Required agent behavior (RFC 2119 MUST/NOT).
* **Values**: Ideal qualities.

## Naming

The name of an item says what kind of commitment it holds, by its grammatical form, and what it must say, by its content; each domain's README states its own scheme in a `## Naming` section:

* Belief: a generic present-tense indicative clause. Environment: a present-tense indicative clause about a particular thing. Expectation: a clause with a futurate or tendency verb.
* Intention: a gerund phrase. Opinion: an evaluative or comparative clause. Value: an abstract noun.
* Practice: an imperative. Principle: a nominalization. Rule: `X MUST Y` or `X SHOULD Y`.

Items that express one idea at a different commitment share a stem, so that the link between them shows in their names: the value "Accurate Anticipation", the intention "Predicting Outcomes Accurately", the principle "Anticipation Before Action" and the practice "State Falsifiable Anticipated Outcomes".

## Lists of Domain Items

For each domain, a list of domain items can be found at `.praxis/domains/${domain}.md`,
with links to more information for each at `.praxis/domains/${domain}/${item-short-name}.md`,
which are created from `.praxis/templates/${domain}-template.md`.

## Domain Item Lifecycles

All domain items follow one of two lifecycles: `.praxis/lifecycles/assertion-lifecycle.md` or `.praxis/lifecycles/evidenced-lifecycle.md`, and `.praxis/domains/${domain}/README.md` will specify which.
