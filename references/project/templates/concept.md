# Project concept-journal authoring template

Cold path: load this file only when creating or materially editing a chronological concept note under `reports/concept/`.

Concept-journal semantics are owned by `../concept.md`; current accepted design is owned by `../design.md`; report filenames/common metadata are owned by `../reports.md`.

## Purpose

A concept note preserves a meaningful piece of design thinking so future work can recover what was considered without contaminating the current living design.

It may contain incomplete ideas, competing alternatives, unresolved questions, design attacks, prior-art findings, or adjudication results.

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

`artifact_id` equals the filename stem.

Do not add `role: design_authority`, version numbers, or implementation projections to concept notes.

## Flexible body shape

Use only the sections useful for the actual idea. A common shape is:

```markdown
# <Concept title>

## Context / problem

## Current observation

## Candidate ideas

## Evidence / prior art

## Attack / counterexamples

## Adjudication

## Design consequence

## Open questions
```

Not every note needs every section.

## Content rules

Good concept-journal material includes:

```text
why a current design became questionable
candidate alternatives and trade-offs
important User constraints or preferences for the decision
external precedent and source pointers
counterexamples that exposed a design gap
what was accepted/rejected/unresolved
which current design topic(s) may need change
```

Do not rewrite the note into a polished description of the final system after the fact. The accepted current result belongs in `design/`.

## Design consequence

When adjudication is sufficiently clear, end with a compact consequence such as:

```text
NO_CHANGE
UPDATE design_id=<...>
NEW_TOPIC <proposed design_id>
SPLIT <design_id>
MERGE <design_id...>
REMOVE <design_id>
REORDER
OPEN — further adjudication required
```

This notation is navigational only. `design.md` owns the actual living-design transformation rules.

## Quality check

A concept note is useful when an unfamiliar future reader can understand the design question, material evidence/alternatives, and disposition without mistaking the note for current authority.
