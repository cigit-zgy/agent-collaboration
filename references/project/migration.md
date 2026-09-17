# Project migration contract

Load this reference when an existing repository itself must be migrated to the current collaboration architecture. This is not normal conversation resume.

Project-wide artifact admission and drift handling are owned by `governance.md`.

## Core distinction

```text
conversation resume
= AGENTS.md → CURRENT.md → optional one current handoff → current owner

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
→ only directly relevant current Design/task/report anchors
```

Do not preload all reports, handoffs, Design topics, Skills, or Concepts.

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

When an older project has divergent Design or overloaded status/report surfaces:

```text
identify every real current responsibility
→ retain/merge only genuine current Design owners
→ remove superseded/duplicate current owners
→ preserve project-specific scientific/canonical artifacts with project-declared owners
→ establish one reports/design/ tree when explicit living Design is used
→ normalize append-only reports/chatgpt + codex + concept + handoff
→ normalize AGENTS/CURRENT/Skill pointers
```

Do not reinterpret scientific/product semantics merely to simplify governance. If consolidation would require choosing meaning, stop that path for User + ChatGPT adjudication.

## Concept handling

Do not create new Concept notes merely to document migration or cleanup.

Existing Concepts remain historical snapshots. New Concept is created only when the User explicitly requests Concept persistence; any accepted current consequence is reflected in Design in the same work unit.

## CURRENT / handoff

For long-running projects, reduce CURRENT to NOW-only state:

```text
current work edge
active coordinates
direct current owner(s)
latest handoff path when applicable
0–3 open edges
one next action
```

When the User explicitly switches conversation after migration, use `handoff.md`; do not create a project-wide recap.

## Reports

Normalize the five recognized active report surfaces:

```text
reports/design/   current mutable Design
reports/chatgpt/  append-only ChatGPT work
reports/codex/    append-only Codex execution
reports/concept/  append-only explicit User-requested history
reports/handoff/  append-only conversation boundaries
```

Do not create `reports/verification/` as a separate family. Maintained checks belong to `tests/`; one-off outputs belong to `tmp/` or cold archive when genuinely worth retaining.

Every Codex task should have a durable ChatGPT task record and a durable Codex execution record.

## Design maintenance

After structural migration, initialize/review the Design reconciliation cursor from `reconciliation.md` when the project uses `reports/design/`.

Do not convert historical reports into Design wholesale. Reduce only accepted current semantics.

## Execution placement

Repository-only migration that connected ChatGPT can safely complete is DIRECT. Use Codex only for genuine local filesystem/runtime/environment evidence.

## Completion

Migration is complete when current authority is singular and routed, historical report families are append-only and correctly classified, CURRENT is pointer-only, current Design has one owner per concern, project-specific artifacts stay with their project-declared owners, and future conversation replacement uses the compact CURRENT/Handoff resume route.
