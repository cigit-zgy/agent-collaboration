# Project Concept authoring template

Cold path: load only after the User has explicitly requested Concept persistence.

Concept semantics are owned by `../concept.md`; current accepted Design lives in `reports/design/` under `../design.md`.

## Preconditions

Before creating a Concept:

```text
User explicitly requested Concept persistence
AND the accepted current Design consequence is known
```

If the Design consequence is still ambiguous, resolve it with the User first.

## File rule

Always create a NEW file:

```text
reports/concept/YYMMDD_concept_NN.md
```

Use the next free sequence for that date. Never overwrite or extend an older Concept with later reasoning.

## Metadata

```yaml
---
artifact_type: project_concept
artifact_id: <YYMMDD_concept_NN>
title: <short title>
date: <YYYY-MM-DD>
project: <PROJECT_NAME>
repository: <OWNER/REPOSITORY>
status: incorporated
summary: >
  <compact historical summary>
design_topics:
  - <design_id>
---
```

Do not add `role: design_authority` or implementation projections.

## Body

Use only the sections needed to preserve the requested reasoning, for example:

```text
Context / problem
Options or evidence
Attack / counterexamples
Adjudication
Accepted Design consequence
```

Do not use Concept for scientific qualification, test evidence, task execution, current status, or ordinary bug-fix history.

## Same-work-unit Design update

After creating the Concept:

```text
update/overwrite the owning reports/design topic(s)
→ update reports/design/README.md when ownership/navigation changes
→ remove superseded current Design owners when needed
```

The Concept write is incomplete until current Design reflects the accepted consequence.
