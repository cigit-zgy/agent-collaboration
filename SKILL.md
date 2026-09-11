---
name: agent-collaboration
description: >
  Coordinate User, ChatGPT, and Codex for repository work involving project or Skill design,
  prior-art research, existing-project migration, multi-conversation resume/current work state,
  direct authoring, local execution, verification, GitHub Actions, Codex delegation/acceptance,
  shared coding-Skill alignment, project integration, exceptional conversation handoff,
  report/archive governance, or Skill maintenance.
---

# Agent Collaboration

Canonical source: `cigit-zgy/agent-collaboration`.

This file is the sole runtime routing index. Read only the owner(s) selected for the active concern.

## Operating model

```text
User    = goals + genuine scientific/product/design/tool decisions + final override
ChatGPT = design partner + connected author/executor + durable Codex-task author + acceptance reviewer
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
| GitHub Actions | `references/collaboration/actions.md` |
| shared coding Skills | `references/collaboration/shared-coding-skills.md` |
| project architecture | `references/project/architecture.md` |
| normal multi-conversation resume / `CURRENT.md` | `references/project/current.md` |
| existing-project migration | `references/project/migration.md` |
| reports/governance layout | `references/project/reports.md` |
| design history / concept notes | `references/project/concept.md` |
| current living design under `reports/design/` | `references/project/design.md` |
| external tool adapters | `references/project/external-tools.md` |
| prior-art/reuse gate | `references/project/prior-art.md` |
| exceptional conversation-only handoff | `references/project/handoff.md` |
| first-party Skill development | `references/skill/development.md` |
| Skill Markdown quality | `references/skill/writing.md` |
| Skill source/distribution | `references/skill/repository.md` |
| Skill package/resources | `references/skill/package.md` |

Use one primary owner plus at most one necessary secondary owner. Templates are cold until creating/reviewing that artifact.

## Project governance model

```text
reports/design/
= what we currently accept
= one canonical living design set
= NOT a chronological report family

reports/concept/
= what we considered
= historical design thinking/input

CURRENT.md
= what we are working on now
= mutable NOW-state only
```

A material new idea changes project authority only after User + ChatGPT adjudication updates `reports/design/`.

## Normal conversation resume

For an integrated long-running project:

```text
old conversation
→ make accepted state repository-native
→ rewrite CURRENT.md
→ create handoff only for unavoidable residual conversation-only delta

new conversation
→ AGENTS.md
→ CURRENT.md
→ reports/design/README.md when present
→ load only the current concern just in time
```

When the User says `换对话框，给我提示词` or equivalent, return only the compact resume prompt defined in `project/current.md`.

Do not preload the full design tree, concept history, old task/report/handoff files, archive, or the collaboration reference tree merely to resume.

## Codex delegation

Every repository task delegated to Codex is first committed under:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

Chat carries only a short immutable locator.

```text
LOCAL-QUICK → committed task → compact result → no reports/codex report
FORMAL      → committed task → reports/codex report → acceptance/integration
```

## Codex remote synchronization

Every repository-changing Codex task:

```text
fresh fetch
→ prove local execution HEAD == authorized fetched baseline
→ mutate
→ commit/push
→ fresh fetch
→ prove local task HEAD == fetched upstream HEAD
→ only then PASS
```

No blind `git pull`, reset, rebase, stash, force checkout, or force push merely to align state.

## Existing-project migration

Project migration is distinct from resume. Older root `design/` trees migrate to `reports/design/` as a path/authority normalization without rewriting project-specific semantics.

## Skill behavior changes

```text
reports/design/ current authority
→ target SKILL.md + references
→ implementation
→ design-probing tests
```

A `DESIGN_GAP` returns to design adjudication before code repair.

## Reports / archive

Recognized `reports/` children are:

```text
reports/design/   current design authority; special non-report-family directory
reports/chatgpt/  durable Codex tasks
reports/codex/    FORMAL execution evidence
reports/concept/  design history/input
reports/handoff/  exceptional conversation-only delta
```

Historical retention uses repository-root `00_archive/` only.

## Cold paths

Do not preload historical concept/task/report/handoff/archive material. For normal resume, orientation is only:

```text
AGENTS.md + CURRENT.md + reports/design/README.md
```

Then retrieve the current owner just in time.

## Completion

Work is complete when durable design/implementation/execution/evidence requirements are satisfied, CURRENT reflects the adopted current work edge when used, remote synchronization evidence is complete for repository-changing Codex work, and required acceptance/User checkpoints are satisfied.
