# Project concept-journal contract

Load this reference when the User explicitly asks to persist a design/scientific discussion or decision in `reports/concept/`, or when reviewing an existing Concept artifact.

Current accepted design lives in `reports/design/` under `design.md`. Project-wide admission, drift, and golden-purity rules live in `governance.md`.

## Core boundary

```text
reports/concept/
= explicitly User-requested chronological historical discussion
= design/scientific reasoning, correction rationale, source reconciliation, qualification reasoning when requested
= append-only
= never current authority

reports/design/
= current accepted design
= one mutable current set

workspace/golden_object/<model>/
= canonical ten-layer structured object only
```

## Creation gate

A new Concept is created only after an explicit User request such as `落实到 Concept`, `写入 Concept`, `记到 Concepts`, or equivalent.

Ordinary discussion, correction, review, qualification, implementation, or execution does not create a Concept by default.

Each accepted request creates a NEW file:

```text
reports/concept/YYMMDD_concept_NN.md
```

Use the next free sequence for that date. Keep the directory flat. Do not overwrite, repurpose, or append later reasoning to an older Concept; later reasoning gets another dated file.

## Concept and Design move together

An explicit Concept persistence request also updates current Design in the same work unit:

```text
new dated Concept
→ accepted current consequence
→ update the owning reports/design topic(s)
→ update reports/design/README.md when ownership/navigation changes
→ remove superseded current-design owners when necessary
```

Do not leave an accepted decision only in Concept. If its current Design consequence is still ambiguous, resolve that ambiguity with the User before committing a misleading Concept/Design pair.

## Concept content

When explicitly requested, Concept may preserve:

```text
problem / question
candidate alternatives
prior-art or source interpretation
scientific correction rationale
source reconciliation
model-specific qualification reasoning
numerical/scientific closure discussion
counterexamples / attacks
User + ChatGPT adjudication
why current Design or golden scientific content changed
```

Concept records the historical reasoning/evidence discussion; it does not become the current source of truth.

Formal Codex command/test/run evidence remains in `reports/codex/`. Raw source files remain with the source/model-source owner. The canonical golden directory remains limited to the ten structured-object layers.

## Design references to Concept

A current Design topic MAY cite exact Concept paths when historical rationale or provenance is useful.

The Design topic must still state the accepted current rule directly. A reader must not need to reconstruct Concept history to determine current semantics.

## Metadata

Use the chronological report naming/metadata contract from `reports.md`. `design_topics` may point to affected current `design_id` values. Concept never carries `role: design_authority`.

Because normal Concept persistence is coupled to a current Design update, `status: incorporated` is the normal completed state when the requested discussion produced an accepted current consequence.

## Historical integrity

Older Concept bodies are historical snapshots and are not rewritten to follow later Design. Git plus the dated Concept series preserve reasoning history; `reports/design/` preserves only the latest accepted state.

## Reading discipline

Routine work reads current Design, not Concept history:

```text
reports/design/README.md
→ relevant current topic(s)
```

Read an exact Concept only when historical rationale/evidence is specifically needed. Never preload the whole Concept journal.

## Collaboration-repository exception

Historical Concept files already present in `agent-collaboration` remain history. Current operational policy lives in `references/` and overrides them.
