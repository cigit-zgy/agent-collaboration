---
name: agent-collaboration
description: >
  Coordinate User, ChatGPT, and Codex for repository work involving project or Skill design,
  prior-art research, governance conformance, existing-project migration, multi-conversation resume,
  direct authoring, local execution, verification, Codex delegation/acceptance, and Skill maintenance.
---

# Agent Collaboration

Canonical source: `cigit-zgy/agent-collaboration`.

Read only the owner(s) selected for the active concern.

## Operating model

```text
User    = goals + scientific/product/design decisions + final override
ChatGPT = design partner + connected author/executor + Codex-task author + acceptance reviewer
Codex   = LOCAL implementation/execution + environment-bound verification/repair; never self-accepts
```

## Direct routing

| Active concern | Primary owner |
|---|---|
| roles/authority/refresh/trust | `references/collaboration/protocol.md` |
| DIRECT/LOCAL/FORMAL, Git/tmp/worktree/sync | `references/collaboration/execution.md` |
| FORMAL task/report/acceptance/integration | `references/collaboration/formal.md` |
| implementation quality | `references/collaboration/implementation.md` |
| verification planning | `references/collaboration/verification.md` |
| project architecture | `references/project/architecture.md` |
| project governance/admission/drift | `references/project/governance.md` |
| normal resume / `CURRENT.md` | `references/project/current.md` |
| existing-project migration | `references/project/migration.md` |
| reports/layout | `references/project/reports.md` |
| explicit User-requested Concept | `references/project/concept.md` |
| current living Design | `references/project/design.md` |
| prior-art/reuse gate | `references/project/prior-art.md` |
| exceptional conversation handoff | `references/project/handoff.md` |
| first-party Skill development | `references/skill/development.md` |

Use one primary owner plus at most one necessary secondary owner. Templates are cold.

## Governance pre-write gate

Before the first substantive repository-changing ChatGPT write in a work unit, inspect the smallest relevant governance surfaces and apply `project/governance.md`.

Deterministic governance drift is repaired before new work expands it. A repair that requires a scientific/product/design choice stops for User + ChatGPT adjudication.

Before issuing a Codex repository task, the governing authority surfaces for that task must conform.

## Project governance model

```text
reports/design/
= current accepted project design
= one current set

reports/concept/
= only explicit User-requested chronological design reasoning
= append-only artifacts

CURRENT.md
= current work edge / NOW only
```

Concept is not a default logging mechanism. ChatGPT creates a Concept only when the User explicitly requests it. Every normal Concept persistence request creates a new dated file and updates current `reports/design/` in the same work unit.

Design is mutable current state: update the real owner and remove superseded current owners rather than stacking design versions.

## Normal conversation resume

```text
AGENTS.md
→ CURRENT.md
→ reports/design/README.md when present
→ load only the current concern just in time
```

When the User says `换对话框，给我提示词` or equivalent, return only the compact resume prompt from `project/current.md`.

## Codex delegation

Every repository task delegated to Codex is first committed under `reports/chatgpt/`. Chat carries only the immutable locator.

```text
LOCAL-QUICK → task → compact result
FORMAL      → task → reports/codex report → acceptance/integration
```

## Codex remote synchronization

Every repository-changing Codex task fresh-fetches before mutation, proves the authorized baseline, then after commit/push fresh-fetches again and proves local task HEAD equals fetched upstream HEAD before PASS.

## Existing-project migration

Project migration is distinct from conversation resume. Migration must reduce governance drift, not merely relocate files. Use `project/migration.md` plus `project/governance.md`.

## Skill behavior changes

```text
reports/design/ current authority
→ SKILL.md + references
→ implementation
→ design-probing tests
```

A `DESIGN_GAP` returns to design adjudication before code repair.

## Cold paths

Do not preload Concept history, old tasks/reports/handoffs, archive, or the full Design tree. Normal orientation is only `AGENTS.md + CURRENT.md + reports/design/README.md`.
