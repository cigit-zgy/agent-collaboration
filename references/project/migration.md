# Project migration contract

Load this reference when an existing repository must be migrated to the current `agent-collaboration` project model.

This is **project-policy migration**, not normal conversation resume. Routine multi-conversation continuity/current work state is owned by `current.md`; exceptional residual conversation-only continuity is owned by `handoff.md`.

## Purpose

Project migration updates an existing repository so its current authority, routing, living design, reports, Skill projection, current-work-state surface, and execution boundaries conform to the current collaboration model **without reconstructing the whole historical conversation or rereading the whole repository**.

The migration prompt is a map, not a manual. Repository-native artifacts remain the system of record.

## Core distinction

```text
conversation resume
= replace one full/old conversation with a fresh conversation
= recover NOW from AGENTS.md + CURRENT.md + design/README.md
= owned by current.md

exceptional handoff
= preserve residual conversation-only delta that has no proper repository owner
= owned by handoff.md

project migration
= change an existing repository to current collaboration architecture/policy
= reconcile repository surfaces against current collaboration
= owned by migration.md
```

Opening a new conversation does not by itself trigger project migration.

## Context-minimization rule — hard boundary

Do not migrate by pasting the project's full history, all concept notes, all Codex reports, or a long prose summary into the new conversation.

Preferred model:

```text
old conversation
→ make important accepted state durable in its real repository owner
→ update CURRENT.md when the project uses it
→ emit a short migration bootstrap only if policy migration is actually needed in a new conversation

new/current conversation
→ resolve current collaboration authority
→ inspect current target repository state
→ load only directly relevant repository-native owners
→ migrate the drifted surfaces
```

## Migration bootstrap

When a new conversation is specifically taking over an unresolved **project-policy migration**, use `templates/migration-bootstrap.md`.

The bootstrap carries only repository coordinates, actual migration objective, current authority/design/CURRENT state, active task/report/branch anchors when relevant, unresolved migration blockers, and unavoidable session-only delta.

Do not summarize collaboration policy or project architecture inside the bootstrap.

## New-conversation migration recovery order

Use the smallest read set:

```text
1. resolve current cigit-zgy/agent-collaboration master;
2. read current collaboration SKILL.md;
3. route directly to project/migration.md;
4. inspect target project AGENTS.md + current branch/HEAD/state;
5. inspect CURRENT.md when present;
6. inspect design/README.md when present;
7. inspect only directly relevant current design/task/report anchors;
8. read historical concept notes only when a specific current design fact must be reconstructed.
```

Do not preload all reports, old handoffs, all design topics, all project Skills/references, or the complete collaboration reference tree.

## Migration assessment first

Before broad edits classify only the surfaces that actually drift:

```text
ALREADY_CONFORMING
ROUTING_DRIFT
CURRENT_STATE_DRIFT
DESIGN_DRIFT
REPORT_DRIFT
SKILL_PROJECTION_DRIFT
IMPLEMENTATION_DRIFT
OPEN_DESIGN
```

`CURRENT_STATE_DRIFT` means a long-running/multi-conversation project lacks a useful root `CURRENT.md`, CURRENT has become a history/status dump, or its pointers contradict current repository state.

## Living-design reconstruction

When `design/` is absent or stale, reconstruct the **single current accepted design state** using the smallest sufficient evidence set:

```text
current project AGENTS / declared authority
→ current supported workflow SKILL.md + references
→ latest accepted repository state and implementation contracts when unambiguous
→ directly relevant incorporated/current concept notes
→ exact active ChatGPT task + Codex report for unresolved execution state
→ exceptional handoff only for residual conversation continuity
→ older history only when a specific unresolved rationale cannot otherwise be recovered
```

Historical concept notes remain history/input. Do not infer implementation correctness merely because code exists.

## CURRENT.md establishment

When the migrated repository is long-running or expected to span multiple conversations, establish/update root `CURRENT.md` under `current.md` after current authority/design/task state is understood.

`CURRENT.md` records only the present work edge and direct pointers. Do not migrate historical status logs into it.

If the project is small/single-session and resume cost is negligible, do not create CURRENT merely for symmetry.

## Delta migration — hard rule

Migrate only surfaces that differ materially from current collaboration.

Typical surfaces:

```text
AGENTS.md authority/routing
CURRENT.md current-work-state surface when justified
repository-root design/ living-design tree
reports/ families + metadata + archive placement
project workflow SKILL.md + references
shared coding-Skill coordinates when used
GitHub Actions/verification placement when implicated
local tmp/worktree policy when stale
```

Do not rewrite already-conforming files for stylistic uniformity alone. Do not change scientific/product semantics merely to make the repository look structurally modern.

## Execution placement

Repository-only migration that can be completed through connected GitHub capability is DIRECT ChatGPT work.

Use Codex only when migration genuinely requires User-machine state, local filesystem/runtime evidence, or environment-bound implementation/verification.

Do not create a Codex task merely because many files need mechanical migration.

## Active-task reconciliation

If the migration bootstrap names an active task/report or BLOCKED state, do not blindly continue it.

```text
re-resolve task/report/branch against current repository state
→ determine whether the blocker remains valid under current design
→ classify OPEN_DESIGN | IMPLEMENTATION_DRIFT | EVIDENCE_GAP | RESOLVED
→ continue only from current authority
```

An old Codex report is execution evidence, not current design authority.

## Migration completion

Project migration is complete when:

```text
current collaboration authority is correctly routed from project AGENTS
AND CURRENT.md is correctly established/omitted under current.md
AND current project design authority is one coherent design/ tree when explicit design is used
AND reports/concept is historical/exploratory input only
AND project Skills/references project current design rather than legacy semantics
AND duplicate/parallel authority surfaces are removed or demoted
AND active task/report/blocker state has been reconciled
AND future conversation replacement can use normal conversation resume rather than rerunning migration
AND no unnecessary historical/context preload was required
```

## Anti-patterns

Do not use:

```text
"new conversation" → automatically rerun project migration
"仔细理解全部历史，然后把整个项目迁移一下"
```

Do not require the new conversation to understand the old conversation before it can inspect the repository. Do not turn the migration bootstrap into a second AGENTS file, CURRENT file, handoff report, design document, or collaboration manual.
