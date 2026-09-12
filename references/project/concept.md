# Project concept-journal contract

Load this reference when the User explicitly asks to persist a design discussion or decision in `reports/concept/`, or when reviewing an existing Concept artifact.

Current accepted design lives in `reports/design/` under `design.md`. Project-wide admission and drift rules live in `governance.md`.

## Core boundary

```text
reports/concept/
= explicitly User-requested chronological design history
= append-only
= never current authority

reports/design/
= current accepted design
= one mutable current set
```

## Creation gate

A new Concept is created only after an explicit User request such as `落实到 Concept`, `写入 Concept`, or equivalent. Ordinary discussion, correction, review, qualification, implementation, or execution evidence does not create a Concept by default.

Each accepted request creates a NEW file:

```text
reports/concept/YYMMDD_concept_NN.md
```

Use the next free sequence for that date. Keep the directory flat. Do not overwrite, repurpose, or append later reasoning to an older Concept; later reasoning gets another dated file.

## Concept and Design move together

An explicit Concept persistence request also updates current Design in the same work unit:

```text
new dated Concept
→ accepted design consequence
→ update the owning reports/design topic(s)
→ update reports/design/README.md when ownership/navigation changes
→ remove superseded current-design owners when necessary
```

Do not leave an accepted decision only in Concept. If its current Design consequence is still ambiguous, resolve that ambiguity with the User before committing a misleading Concept/Design pair.

## Concept content

When explicitly requested, Concept may preserve the problem, alternatives, relevant prior art, counterexamples, adjudication, and why the accepted Design changed.

Do not use Concept as the owner of scientific qualification, golden-object closure, test/evaluation evidence, Codex execution evidence, current status, bug-fix logs, or source-transcription logs. Route those to their actual scientific/task/report/current owner.

## Metadata

Use the chronological report naming/metadata contract from `reports.md`. `design_topics` may point to affected current `design_id` values. Concept never carries `role: design_authority`.

Because normal Concept persistence is coupled to a current Design update, `status: incorporated` is the normal completed state.

## Historical integrity

Older Concept bodies are historical snapshots and are not rewritten to follow later Design. Git plus the dated Concept series preserve reasoning history; `reports/design/` preserves only the latest accepted state.

## Reading discipline

Routine work reads current Design, not Concept history:

```text
reports/design/README.md
→ relevant current topic(s)
```

Read an exact Concept only when historical rationale is specifically needed. Never preload the whole Concept journal.

## Collaboration-repository exception

Historical Concept files already present in `agent-collaboration` remain history. Current operational policy lives in `references/` and overrides them.
