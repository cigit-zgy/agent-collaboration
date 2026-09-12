# Project migration contract

Load this reference when an existing repository itself must be migrated to the current collaboration architecture. This is not normal conversation resume.

Project-wide artifact admission, golden purity, and drift handling are owned by `governance.md`.

## Core distinction

```text
conversation resume
= AGENTS.md → CURRENT.md → reports/design/README.md

project migration
= repository architecture/policy reconciliation
```

Opening a new conversation does not trigger project migration.

## Recovery set

Use only:

```text
current agent-collaboration SKILL.md
→ project/migration.md + project/governance.md
→ target AGENTS.md + branch/HEAD/state
→ CURRENT.md when present
→ reports/design/README.md when present
→ only directly relevant current design/task/report anchors
```

Do not preload all reports, handoffs, design topics, Skills, or historical Concepts.

## Assessment

Classify only real drift:

```text
ALREADY_CONFORMING
GOVERNANCE_DRIFT
DESIGN_ARCHITECTURE_DRIFT
ROUTING_DRIFT
CURRENT_STATE_DRIFT
DESIGN_DRIFT
REPORT_DRIFT
SKILL_PROJECTION_DRIFT
IMPLEMENTATION_DRIFT
OPEN_DESIGN
```

## Structural reduction before relocation

Migration is not a mechanical folder move.

When an older project has a divergent root `design/` tree or overloaded Concept/CURRENT/report surfaces:

```text
classify every current design artifact by real responsibility
→ retain/merge only genuine current project-design owners
→ remove superseded/duplicate current owners from the current set
→ keep raw registered source material with source/model-source owners
→ move historical model-specific scientific reasoning to Concept only when the User explicitly directs Concept persistence
→ keep canonical golden directories restricted to their structured-object files
→ establish one reports/design/ tree
→ normalize AGENTS/CURRENT/Skill pointers
→ normalize chronological report names/layout
```

Do not move a divergent `design/` tree unchanged into `reports/design/` and call the migration complete.

Do not relocate removed Design documents, scientific qualification narratives, correction records, or numerical audit scripts into `workspace/golden_object/<model>/evidence/` or another golden sidecar. Golden-object directories remain pure scientific-object surfaces under `governance.md`.

Do not reinterpret scientific/model semantics merely to simplify governance. If consolidation would require a scientific/product/design choice, stop that path for User + ChatGPT adjudication.

## Concept handling during migration

Do not create new Concept notes merely to document migration or cleanup.

Existing Concept files remain historical snapshots. A new Concept is created only if the User explicitly requests Concept persistence under `concept.md`; when that happens, update current Design in the same work unit.

When the User explicitly directs historical model-specific reasoning/evidence into Concept, create new canonical Concept artifact(s) without overwriting existing Concept history, then update current Design to the accepted consequence.

Migration may normalize non-canonical Concept filenames/metadata without rewriting historical reasoning.

## Golden-object handling during migration

For a project using canonical ten-layer structured objects:

```text
workspace/golden_object/<model>/
= Layer 01–10 files only
```

Migration may remove non-golden sidecars from that directory, but must not alter the ten-layer scientific semantics merely to satisfy governance.

Historical reasoning removed from a golden sidecar goes to Concept only when the User has explicitly requested that persistence. Formal execution evidence belongs in `reports/codex/`; raw source artifacts remain with source/model-source owners.

## CURRENT.md

For long-running projects, reduce CURRENT to pointer-only NOW-state under `current.md`:

```text
current work edge
active coordinates
direct current owners
0–3 open edges
one next action
```

Do not carry model closure narratives, test summaries, completed-task history, or parallel-work diaries into CURRENT.

## Reports

Chronological report families are `chatgpt`, `codex`, `concept`, and `handoff`; filenames use `YYMMDD_<family>_NN.md`.

Normalize non-canonical names without changing historical substance. `reports/design/` is current authority, not a chronological report family.

## Execution placement

Repository-only migration that connected ChatGPT can safely complete is DIRECT. Use Codex only for genuine local filesystem/runtime/environment evidence.

## Completion

Migration is complete only when:

```text
project AGENTS routes authority correctly
AND governance.md conformance checks pass for the migrated surfaces
AND CURRENT is pointer-only or deliberately absent
AND one current reports/design/ tree exists when Design is used
AND every current Design concern has one owner
AND no superseded/parallel Design owner remains
AND Concepts remain explicit-User historical artifacts only
AND raw source material, Concept history, current Design, execution evidence, and golden objects have distinct owners
AND canonical golden directories contain only their structured-object layer files
AND chronological report names/layout conform
AND Skill/references project current Design
AND future conversation replacement uses normal resume
```
