# Project concept-journal contract

Load this reference for chronological design exploration under `reports/concept/`: recording ideas, alternatives, unresolved questions, prior-art findings, design attacks, and the adjudication that may later update the canonical `design/` tree.

Current accepted design authority is owned by `design.md`. Report-family filenames/metadata are owned by `reports.md`. When authoring a concept note, also load `templates/concept.md`.

## Core distinction — hard boundary

```text
reports/concept/
= what we considered and how the design evolved
= chronological design journal
= evidence/input for design adjudication
= NOT current design authority

design/
= what the project currently accepts
= canonical living design authority
= current state only
```

A concept note may be exploratory, incomplete, contain competing options, or later become obsolete. Its existence does not authorize implementation.

## Concept-journal responsibility

Use `reports/concept/` when a discussion is worth preserving because it may help future design work recover:

```text
a new design idea or requirement
an identified design defect or ambiguity
candidate A/B/C approaches
prior-art findings and reuse/adapt/reject reasoning
an adversarial review or counterexample
an unresolved design question
why an accepted design was changed or left unchanged
why a plausible approach was rejected
```

Do not force a concept note into polished current-system prose. The journal exists specifically so exploratory reasoning does not pollute `design/`.

## Filename and chronology

Concept notes follow the report-family naming contract:

```text
reports/concept/YYMMDD_concept_NN.md
```

`NN` is the two-digit sequence for that date/family. Files remain flat under `reports/concept/`.

Chronology lives in filenames/date metadata. Semantic links to current design may be carried by optional topic identifiers; concept filenames do not become current design filenames.

## Metadata

Use the common report metadata from `reports.md` plus only concept-specific fields that improve recovery:

```yaml
---
artifact_type: project_concept
artifact_id: <YYMMDD_concept_NN>
title: <short title>
date: <YYYY-MM-DD>
project: <project name>
repository: <owner/repository>
status: <open | incorporated | rejected | superseded | recorded>
summary: >
  <compact searchable summary>
design_topics:
  - <design_id>   # optional; only known affected current concern(s)
---
```

`artifact_id` equals the filename stem.

Do not use `role: design_authority` for concept notes. Do not require `operational_projection`; implementation projection belongs to the accepted living design.

A note may start as `open`. After adjudication, its status may be updated to `incorporated`, `rejected`, `superseded`, or `recorded` when useful for retrieval. Updating status does not rewrite the historical reasoning into a different conclusion.

## Writing shape

Concept notes are intentionally flexible. A useful note often contains only the sections needed for the actual discussion, for example:

```text
Context / problem
Current observation
Candidate ideas
Evidence / prior art
Attack / counterexample
User + ChatGPT adjudication
Design consequence
Open questions
```

These are optional shapes, not mandatory headings.

The important separation is:

```text
exploration / alternatives / history
→ concept note

accepted current semantics
→ design/
```

## Prior-art relationship

For a gate-triggered new project/core design, `prior-art.md` is completed before substantial custom design is accepted.

The detailed search trail, strongest candidates, `REUSE | ADAPT | REFERENCE_ONLY | REJECT` reasoning, and unresolved findings may be recorded in one or more concept notes.

Only the accepted current consequence is then reduced into `design/`.

## Adjudication and reduction into design

A concept note does not automatically produce a design change.

User + ChatGPT adjudicate the material and classify its current-design consequence using `design.md`:

```text
NO_CHANGE
UPDATE
NEW_TOPIC
SPLIT
MERGE
REMOVE
REORDER
```

When the result changes accepted design:

```text
concept note(s)
→ User + ChatGPT adjudication
→ update design/ into one coherent current state
→ update SKILL.md/references projection
→ implementation
→ tests/evidence
```

When the result is `NO_CHANGE`, retain the concept note as useful history and leave `design/` unchanged.

## Historical integrity

Issued concept notes are historical reasoning artifacts. Do not continuously rewrite their bodies to look like the current design.

If a later idea contradicts an earlier note, create a new dated concept note and update living design only after adjudication. Git history plus the journal preserve evolution.

Old concept notes are not moved into `design/`, and superseded design files are not moved into `reports/concept/`; these are different artifact families with different responsibilities.

## Reading routes

Routine project execution SHOULD NOT read concept history when operational projection is already sufficient.

For current design:

```text
AGENTS.md
→ design/README.md
→ relevant current design topic(s)
```

For historical rationale or a new design discussion:

```text
current design topic
+ relevant reports/concept note(s) only when needed
→ adjudication
→ design update if accepted
```

Do not preload the entire concept journal.

## Current-design authority

All freeze/reopen/current-structure semantics belong to `design.md`.

A design concern is ready for implementation only when its current accepted semantics are represented in `design/` and downstream projection can be written without inventing missing choices.

## Roadmap/status boundary

`reports/concept/` is not an execution backlog or implementation-status board. Task execution belongs in ChatGPT/Codex task/report artifacts or another explicitly declared work-management surface.

## Collaboration-repository exception

`agent-collaboration` itself uses `reports/concept/` as its design-decision history. Its current operational policy remains under `references/`; concept history never overrides current runtime policy.
