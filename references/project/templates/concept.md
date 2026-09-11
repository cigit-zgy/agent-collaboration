# Project concept-journal authoring template

Cold path: load only when creating/editing a concept note under `reports/concept/`.

Concept semantics are owned by `../concept.md`; current accepted design lives in `reports/design/` under `../design.md`.

## Purpose

A concept note preserves meaningful design thinking—ideas, alternatives, unresolved questions, attacks, prior art, or adjudication—without contaminating current living design.

It is not design authority.

## Required metadata

```yaml
---
artifact_type: project_concept
artifact_id: <YYMMDD_concept_NN>
title: <short title>
date: <YYYY-MM-DD>
project: <PROJECT_NAME>
repository: <OWNER/REPOSITORY>
status: <open | incorporated | rejected | superseded | recorded>
summary: >
  <compact searchable summary>
design_topics:
  - <design_id>   # optional
---
```

Do not add `role: design_authority`, version numbers, or implementation projections.

## Flexible body

Use only useful sections, for example:

```text
Context / problem
Current observation
Candidate ideas
Evidence / prior art
Attack / counterexamples
Adjudication
Design consequence
Open questions
```

Do not rewrite the note after the fact into a polished current-system description. Accepted current semantics belong in `reports/design/`.

## Design consequence

A compact disposition may be:

```text
NO_CHANGE
UPDATE design_id=<...>
NEW_TOPIC <design_id>
SPLIT <design_id>
MERGE <design_id...>
REMOVE <design_id>
REORDER
OPEN — further adjudication required
```

`design.md` owns the actual transformation rules.
