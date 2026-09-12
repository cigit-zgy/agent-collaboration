# Project governance conformance contract

Load this reference when creating/changing project governance artifacts, normalizing a repository to the collaboration model, or when authority/artifact drift is suspected.

This contract is a pre-write conformance gate. It does not replace `design.md`, `concept.md`, `current.md`, `reports.md`, scientific source authority, or project-specific golden-object semantics.

## Purpose

Prevent locally reasonable edits from accumulating into repository-wide authority drift.

Before the first substantive repository-changing ChatGPT write in a work unit, inspect only the governance surfaces relevant to that work and verify the hard invariants below. Before issuing a Codex repository task, the task's governing authority surfaces must also conform.

Do not perform a full historical audit for every small edit. Check the smallest set that can establish the active authority and artifact owner.

## Hard conformance gate

### 1. One current design location

When explicit living design is used:

```text
reports/design/
= the only current living-design tree
```

A root `design/`, `design_v2/`, dated design tree, draft/backup design tree, or another parallel current design location is non-conforming.

### 2. One concern, one current owner

Every current design concern has exactly one owning topic.

A current design topic is non-conforming when it primarily:

```text
is superseded by another current topic
refines/overrides another current topic for the same semantic responsibility
keeps a previous version beside its replacement
defines the same rule independently in multiple current files
```

Cross-topic interfaces are allowed; duplicate semantic ownership is not.

For one bounded concern, the normal read set is one primary current design owner plus at most one genuinely necessary secondary owner. If establishing one rule routinely requires three or more current design topics, classify `DESIGN_ARCHITECTURE_DRIFT` and consolidate ownership before adding more design files.

### 3. Artifact admission

Route durable information by responsibility:

```text
accepted current project design                → reports/design/
registered source bytes / source corpus         → project source/model-source owner
historical scientific/design reasoning          → reports/concept/ only under the explicit-User Concept gate
ChatGPT delegated task                          → reports/chatgpt/
FORMAL implementation/verification evidence     → reports/codex/
current work edge                               → CURRENT.md
exceptional conversation-only delta             → reports/handoff/
canonical model golden structured object        → project golden-object owner under the Golden purity rule below
```

Do not use one artifact class as a convenient container for another responsibility.

### 4. Concept creation requires explicit User instruction

ChatGPT MUST NOT autonomously create a concept note merely because a discussion, correction, experiment, qualification, review, or implementation result seems worth preserving.

Create a new concept artifact only when the User explicitly instructs something equivalent to:

```text
落实到 Concept
写入 Concept
记到 Concepts
把这个设计讨论保存到 Concept
```

When the User explicitly requests Concept persistence:

```text
create a NEW reports/concept/YYMMDD_concept_NN.md
→ never overwrite or repurpose an existing concept artifact
→ record the requested historical reasoning/decision/evidence discussion at that scope
→ in the SAME work unit update reports/design/ to the resulting current accepted design
→ update reports/design/README.md when topic ownership/navigation changes
```

Concept is append-only historical discussion. Design is mutable current state.

Scientific correction rationale, source reconciliation, golden qualification reasoning, and similar historical scientific discussion MAY live in Concept when the User explicitly asks to preserve it there. Formal command/test/run evidence remains in `reports/codex/`; raw source material remains with the source owner.

A Concept write is not complete while an accepted current consequence remains only in Concept. If the requested decision cannot yet be represented unambiguously in current design, stop for User + ChatGPT adjudication before committing a misleading concept/design pair.

### 5. Living design is current-only and replace-in-place

`reports/design/` maintains one current normal form.

When accepted design changes:

```text
update/overwrite the owning current topic(s)
→ merge/split/remove/reorder when responsibility changes
→ remove superseded current files
→ keep history in Git and explicit Concept artifacts only
```

Design MAY cite exact Concept artifacts for historical rationale/provenance, but the current rule must remain understandable from Design without requiring historical Concept reconstruction.

Do not preserve old design content beside the replacement for history.

### 6. Golden object purity — hard boundary

When a project uses canonical ten-layer golden structured objects, the golden directory is a scientific object surface, not an evidence/history container.

For each model:

```text
workspace/golden_object/<model>/
```

contains exactly the canonical ten structured-object layer artifacts and no other project-authored material.

Admitted content is only the project's canonical Layer 01–10 files, for example:

```text
01_object_identity.yaml
02_state_variable_declaration.yaml
03_derived_variable_declaration.yaml
04_parameter_declaration.yaml
05_process_declaration.yaml
06_stoichiometric_structure.yaml
07_kinetic_structure.yaml
08_derived_structure.yaml
09_boundary_interface_specification.yaml
10_consistency_constraints.yaml
```

The golden directory MUST NOT contain:

```text
evidence/
README or notes
qualification/correction reports
source-comparison records
numerical check scripts
validation outputs
source PDFs or source copies
manifests added only for audit/history
old/superseded golden snapshots
```

Ownership is:

```text
raw/registered sources                    → source/model-source owner
historical scientific reasoning           → reports/concept/ when explicitly requested by the User
current accepted representation contract  → reports/design/
FORMAL execution/verification evidence     → reports/codex/
canonical golden object                    → ten Layer 01–10 files only
```

A Design topic may cite the exact Concept artifact that records historical scientific reasoning, but neither Design nor Concept is copied into the golden directory.

### 7. CURRENT is pointer-only

`CURRENT.md` stores NOW only: current work edge, direct owner/task/report coordinates, at most three open edges, and one next action.

Target `<= 4 KiB`. Above `8 KiB` is non-conforming unless a project-specific authority explicitly justifies it. Move leaked scientific detail, design semantics, evidence, history, or backlog content to the owning artifact.

### 8. Reports conform mechanically

Chronological report families are exactly:

```text
reports/chatgpt/
reports/codex/
reports/concept/
reports/handoff/
```

Their Markdown filenames match:

```text
YYMMDD_<family>_NN.md
```

`reports/design/` is the sole non-chronological governance directory under `reports/` and is governed by `design.md`.

Non-canonical report names or extra active report families are governance drift; normalize them without rewriting historical substance.

## Drift response

Classify detected violations before continuing:

```text
GOVERNANCE_DRIFT
= deterministic authority/path/admission/naming/current-state/golden-purity violation
→ repair governance first
→ then continue the original bounded work

DESIGN_ARCHITECTURE_DRIFT
= current design ownership is duplicated/over-fragmented/superseded in place
→ consolidate current design before adding new design semantics

SCIENTIFIC_OR_DESIGN_AMBIGUITY
= repair would require choosing scientific/product/design meaning
→ stop affected path
→ User + ChatGPT adjudicate
```

Do not use a governance cleanup to silently change scientific/model semantics.

## Migration / repository normalization

When normalizing an existing repository, prefer structural reduction over mechanical relocation:

```text
classify each current design artifact by real responsibility
→ keep/merge only genuine current generic/project design owners
→ move historical model-specific reasoning to Concept only when the User explicitly requires Concept persistence
→ keep raw model/source material with source/model-source owners
→ keep golden directories restricted to their canonical structured-object files
→ remove superseded/duplicate current design owners
→ preserve existing historical reasoning in existing Concept/Git history
→ shrink CURRENT to pointers
→ normalize report names/layout
→ update AGENTS/Skill routing
```

Moving a divergent `design/` tree unchanged into `reports/design/`, or moving removed Design files into a golden `evidence/` directory, is not sufficient conformance.

## Completion

A project governance state conforms when:

```text
one current reports/design/ tree exists when design is used
AND each current design concern has one owner
AND Concept creation occurred only under explicit User instruction
AND every new Concept has its accepted consequence reflected in current Design
AND Concept history is append-only while Design is current-only/mutable
AND raw sources, historical reasoning, current design, execution evidence, and golden objects have distinct owners
AND every canonical ten-layer golden directory contains only Layer 01–10 artifacts
AND CURRENT is pointer-only
AND chronological report families conform mechanically
AND bounded work can reach its design owner without a multi-owner reading chain
```
