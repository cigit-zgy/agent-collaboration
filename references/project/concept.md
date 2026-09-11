# Project concept-journal contract

Load this reference for chronological design exploration under `reports/concept/`: ideas, alternatives, unresolved questions, prior-art findings, design attacks, and adjudication history.

Current accepted design authority is owned by `design.md` and lives under `reports/design/`.

## Core distinction

```text
reports/concept/
= what we considered / how design thinking evolved
= chronological history/input
= never current authority

reports/design/
= what the project currently accepts
= one canonical living design set
= current state only
```

A concept note may be exploratory, incomplete, contradictory, rejected, or later superseded. Its existence does not authorize implementation.

## Responsibility

Use concept notes for material worth preserving, such as new design ideas/requirements, identified gaps, candidate A/B/C approaches, prior-art findings, attacks/counterexamples, unresolved design questions, and reasons an accepted design changed or did not change.

Do not force concept notes into polished current-system prose; that belongs in `reports/design/`.

## Filename and metadata

Concept notes use:

```text
reports/concept/YYMMDD_concept_NN.md
```

with the common report metadata plus optional `design_topics` identifiers.

Do not use `role: design_authority` or require `operational_projection` in concept notes.

## Adjudication

User + ChatGPT classify a material concept's effect on current design through `design.md`:

```text
NO_CHANGE
UPDATE
NEW_TOPIC
SPLIT
MERGE
REMOVE
REORDER
```

When accepted design changes:

```text
reports/concept note(s)
→ User + ChatGPT adjudication
→ update reports/design/ into one coherent current state
→ update Skill/reference projection
→ implementation
→ tests/evidence
```

When result is `NO_CHANGE`, keep the concept as history and leave `reports/design/` unchanged.

## Historical integrity

Do not continuously rewrite historical concept bodies to match current design. Later contradictions get a new dated concept note; living design changes only through current `reports/design/` updates.

Do not move old concept notes into `reports/design/`, and do not keep superseded design copies inside `reports/design/`.

## Reading routes

Current design:

```text
AGENTS.md
→ reports/design/README.md
→ relevant current topic(s)
```

Historical rationale/new design discussion:

```text
current reports/design topic
+ exact relevant reports/concept note(s)
→ adjudication
→ reports/design update if accepted
```

Do not preload the whole concept journal.

## Collaboration-repository exception

`agent-collaboration` itself keeps design-decision history in `reports/concept/`, while its current operational policy lives in `references/`; historical concept notes never override current runtime policy.
