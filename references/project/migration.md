# Project migration contract

Load this reference when an existing repository itself must be migrated to the current collaboration architecture. This is not normal conversation resume.

Project-wide artifact admission and drift handling are owned by `governance.md`.

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
→ keep model/source-specific scientific facts with their scientific/model/golden owners
→ establish one reports/design/ tree
→ normalize AGENTS/CURRENT/Skill pointers
→ normalize chronological report names/layout
```

Do not move a divergent `design/` tree unchanged into `reports/design/` and call the migration complete.

Do not reinterpret scientific/model semantics merely to simplify governance. If consolidation would require a scientific/product/design choice, stop that path for User + ChatGPT adjudication.

## Concept handling during migration

Do not create new Concept notes merely to document migration or cleanup.

Existing Concept files remain historical snapshots. A new Concept is created only if the User explicitly requests Concept persistence under `concept.md`; when that happens, update current Design in the same work unit.

Migration may normalize non-canonical Concept filenames/metadata without rewriting historical reasoning.

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
AND scientific facts/evidence/task results live with their real owners
AND chronological report names/layout conform
AND Skill/references project current Design
AND future conversation replacement uses normal resume
```
