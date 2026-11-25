---
name: praxis-flow-introspect
description: Analyze the whole history of tracking, domains, factory products, and past runs for new Patterns, skill candidates, Signals, contradictions, blind spots, and domain updates that praxis-flow-learn cannot see; score the last introspection's forecasts and write new ones. Use when the user asks for introspection, or after many Flow runs have been recorded.
confidence: Low
complexity: Qualitative
---

# Skill: Praxis Introspect

Look across many Flow runs, not just the current one, for what the agent has not yet noticed about itself.

## Origin
Praxis Template

## Purpose
Find Patterns, skill candidates, Signals, confidence changes, contradictions, and domain updates that only show up in the history of tracking, the domains, the factory, and past runs.

## When to Use
When the user asks for introspection, or after several Flow runs have been recorded since the last one. It is not part of every run; for a lighter, ad-hoc assessment use `praxis-flow-self-review`. Run it as a Pattern inside a Plan so that it passes through Predict, Discern, and Reflect like other work.

## How it Works
`praxis-flow-learn` reviews the Analyses of the current run. This skill reviews the record of all runs: the confidence tables, signals, domain items, factory products, and the git history of `.praxis/`, including the state of earlier runs as it was committed before each `Clear state` commit. It also holds itself to account: it scores the forecasts the last introspection made, compares what the owner had to point out with what the runs' own Analyses caught, and ends with forecasts of its own for the next introspection to score. It grades each finding by the strength of its evidence, separates what can be written to tracking now from what needs the user's consent, and never changes a domain item or promotes a factory product itself.

Patterns need independent uses: several uses inside one run count as one observation. When history is thin, the right result is a short report that says so.

## Requirements
`.praxis/` is under git. Findings need history: with commits from only one or two Flow runs, report that, give only what that history supports, and do not infer trends.

## Inputs
- Introspections: the items in `.praxis/tracking/introspections/` and their list `.praxis/tracking/introspections.md` (`.praxis/lifecycles/introspection-lifecycle.md`), read and written by hand
- Tracking: `.praxis/tracking/confidence/*.csv`, `.praxis/tracking/confidence.md`, `.praxis/tracking/signals.md`, and `.praxis/tracking/signals/*.md`
- Domains: `.praxis/domains/*.md` and `.praxis/domains/*/*.md`
- Factory: `.praxis/factory/*.md`, `.praxis/factory/patterns/*.md`, and the products listed there
- History: `git log -p` and `--numstat` for those paths, and the committed `.praxis/state/` files of earlier runs (read at the commit before each `Clear state`)
- Lifecycles and templates in `.praxis/lifecycles/` and `.praxis/templates/`
- Optionally, a time window or focus area from the user

## Procedure
1. Set the scope. The scope is the runs recorded after the last introspection's marker, or all history if there is none, narrowed to any window or focus the user gave. Count the independent Flow runs in scope (each ends at a `Clear state` commit) and state that number. Note events git does not hold: compactions of the conversation, and work done outside any run.
2. Score the earlier introspections with `.praxis/factory/skills/praxis-refine-introspection/SKILL.md`: it scores every Recorded item's forecasts as Hit, Miss, or Too early, writes the scores into each item, moves an item to Scored when every forecast is final, and notes what each Miss shows. A Miss is a finding about introspection itself: what the forecast assumed and what happened instead, and whether the finding behind it was wrong or its fix did not work. Forecasts that are all Hits on easy targets are a finding too (introspection is not risking anything). The record of introspection over time is the scores of every Recorded item taken together.
3. Confidence history. For each subject in `.praxis/tracking/confidence/*.csv`, follow its level through `git log -p`. Look for levels that changed without evidence matching `.praxis/lifecycles/confidence-lifecycle.md`, subjects that swing up and down, subjects stuck at one level despite use, and rows with no matching item or product. Propose corrected levels with the evidence.
4. Patterns. In the Plans and Outcomes of past runs, look for sequences of Patterns, tasks, tools, or skills that recur across independent runs and are not yet in `.praxis/factory/patterns/`. Also look for Patterns that are never used, always used together (candidates to merge), or behave differently in different contexts (candidates to split). Propose new Patterns at Low confidence, and lifecycle changes for existing ones.
5. Skill, script, and agent candidates. For Patterns at Medium confidence or higher that are repeatable and nameable, judge the complexity level (`.praxis/factory/README.md`) and propose the matching `praxis-create-*` product. Propose promotion of Unstable products that have reached High (`praxis-promote-factory`), and retirement of products that are never used. Then search every factory product for parts that need a lower level than their product gives them, over all recorded runs. Triage each candidate: a Small candidate whose product is Unstable is Write now, as a Task; any other is For the owner.
6. Signals. Compute from the Analyses of past runs: the share of Results that were Accurate or Helpful, Harmful, and surprising, the share of Plans that were Revised or Rejected, and recurring domain misalignment. Compare with `.praxis/tracking/signals/`. Propose new Signals and updates to existing ones, with the values and the runs they came from.
7. Domain history. From the commits and Analyses, look for:
   - items that change often (candidates for Questioned or Challenged)
   - items that repeatedly appear as Ambiguous, Contradictory, or Unaligned
   - items no Plan, Prediction, or Analysis ever refers to
   - a recurring misalignment that no item covers (candidate for a new item)
   - evidence that justifies a lifecycle move (see `praxis-promote-assertion` and `praxis-promote-evidenced`)
   - overlapping items whose wording has drifted apart
8. Contradictions. Look for contradictions within and between domains, between tracking and the domains (for example a confidence level that disagrees with an item's status), and between lifecycles, templates, and skills. Treat each as informative. Present a contradiction between domain items as thesis, antithesis, and a proposed synthesis (see `.praxis/glossary.md`).
9. Cohesion and conformance. Check that each list (`.praxis/domains/*.md`, `.praxis/factory/*.md`) names exactly the files that exist, that each tracked subject has an item and each item has a tracking row where one is required, that every Domain Alignment reference resolves, and that each skill's `name` equals its directory. Then audit each run in scope against the Flow: each state item filled in from its template, each item taken through every stage of its lifecycle, Tasks written before the work, and Discern a step of its own. Record a failure the run did not record in its own Analysis as a finding of its own.
10. Blind spots. List the owner's prompts since the scope's first commit and mark each that corrects the agent, reverses its work, or reports a problem the agent had not reported ("something strange happened", "back out", "that's not what I meant"). For each, look in the Analyses of the run it fell in, and the run before, for the same problem recorded before the owner said it (in Surprises, Unfulfilled or Domain Misalignment). A problem the owner caught and no Analysis recorded is a blind spot: record it as a finding of its own, Strong, with the prompt's time and the run, and say what in the Flow should have caught it. Then do the same for the instruments: a problem a Signal or a check measured in a run whose Analyses never mention it was measured but not read. State the number of blind spots, or "none" with the number of prompts compared.
11. Triage. For every finding record its kind, the evidence (files and commits), its strength (Weak, Moderate, or Strong), the proposal, and how it applies:
   - **Write now**: a tracking change (confidence, Patterns, or Signals) that the lifecycle's evidence supports.
   - **For the owner**: a promotion or retirement of a factory product, and a domain change the agent judges, case by case, to need the owner's word (`CLAUDE.md`).
   - **Report only**: the evidence is too weak to act on.
12. Forecast. Write this introspection's item with `.praxis/factory/skills/praxis-create-introspection/SKILL.md`: three to five falsifiable forecasts about the runs after this one, each tied to a finding (what a fix should move, or what will go on happening if nothing changes), with the scope marker, the run count, and the blind spots. Later introspections score them at step 2.
13. Record the findings, the scores of step 2, the blind spots and the forecasts as the Outcome of the Plan using `.praxis/templates/outcome-template.md`, and hand the consent-requiring proposals to `praxis-flow-learn`, to be included in its review.
14. Check the mechanical parts of the steps above by reading the run history (the scope and scores, the recorded runs and Signals, and the owner's prompts and side questions since the scope's first commit) and by checking cohesion and conformance, every check against what it passed before; check their numbers against what you read.

## Output
Findings, the scores of the earlier introspections' forecasts, and the blind spots recorded in the Plan's Outcome; this introspection's item in `.praxis/tracking/introspections/`, Recorded; tracking updates written for the findings that need no consent; and proposals for domain changes, promotions, and new factory products, ready for `praxis-flow-learn`.

## Success Criteria
- The number of independent runs in scope is stated.
- Every finding cites evidence (files and commits), and a kind with no findings is stated as "none".
- No factory product was promoted without the user's consent, and every domain change was named for `praxis-flow-learn`.
- Evidence from one run is not presented as a pattern.
- Every Recorded introspection item is scored, or there was none; this introspection's item holds three to five forecasts that parse.
- The number of blind spots is stated, with the number of the owner's prompts compared.

## Domain Alignment

None recorded yet; the domain lists are still being populated.

## Related Skills

- praxis-flow-self-review
- praxis-flow-learn
- `.praxis/factory/skills/praxis-create-introspection/SKILL.md` and `.praxis/factory/skills/praxis-refine-introspection/SKILL.md` (uninstalled, named by path)
- praxis-flow-analyze
- praxis-flow-plan
- praxis-flow-record
- praxis-flow-report
- praxis-promote-assertion
- praxis-promote-evidenced
- praxis-promote-factory

## Troubleshooting

### Issue: Too little history

Identifying:
The scope contains fewer than three independent Flow runs.

Solution:
Say so. Report confidence-level checks and cohesion problems, which need no history, and mark everything else "insufficient history". Do not propose Patterns or new products.

### Issue: A finding rests on a single run

Identifying:
Every piece of evidence for a Pattern, trend, or Signal is from one Flow run.

Solution:
Record it as Weak and report only; do not propose a Pattern or a lifecycle change.

### Issue: A finding duplicates what praxis-flow-learn already proposed

Identifying:
The same change appears in this run's Analyses.

Solution:
Leave it to `praxis-flow-learn` and note that it was found there.

### Issue: A finding contradicts something the user stated directly

Identifying:
The evidence argues against an item created from a user statement.

Solution:
Do not propose demoting or removing it on the agent's authority. Present the evidence as a contradiction (thesis, antithesis, synthesis) and let the user decide.

### Issue: The scope is too large to read in full

Identifying:
The history is long enough that reading every commit is impractical.

Solution:
Narrow by path or period, state what was left out, and offer a second pass.
