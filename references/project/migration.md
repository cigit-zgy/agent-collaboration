# Project migration contract

Load this reference when an existing repository itself must be migrated to the current collaboration architecture. This is not normal conversation resume.

## Core distinction

```text
conversation resume
= AGENTS.md → CURRENT.md → reports/design/README.md
= owned by current.md

exceptional handoff
= residual conversation-only delta
= owned by handoff.md

project migration
= repository architecture/policy reconciliation
= owned here
```

Opening a new conversation does not trigger project migration.

## Context-minimization rule

Do not paste project history into the migration prompt. Repository-native artifacts are the system of record.

Migration recovery uses:

```text
1. current agent-collaboration SKILL.md
2. project/migration.md
3. target AGENTS.md + branch/HEAD/state
4. CURRENT.md when present
5. reports/design/README.md when present
6. only directly relevant current design/task/report anchors
7. historical concept notes only for a specific unresolved rationale
```

Do not preload all reports, handoffs, design topics, project Skills, or collaboration references.

## Assessment

Classify only real drift:

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

## Living-design path migration

The current design location is:

```text
reports/design/
```

When an older project uses repository-root `design/`, migrate the single current tree to `reports/design/`.

This is a path/authority migration only:

```text
root design/
→ reports/design/
```

Preserve current topic files/semantics; update only path-dependent pointers such as AGENTS, CURRENT, Skill/reference owners, tasks, and navigation links.

Do not convert concept notes into one-to-one design files and do not rewrite scientific/product semantics merely for layout consistency.

If the current design must be reconstructed, use the smallest sufficient evidence set:

```text
current AGENTS / declared authority
→ current supported Skill/references
→ unambiguous current repository contracts
→ directly relevant concept notes
→ exact active task/report when needed
→ exceptional handoff only for residual continuity
```

## CURRENT.md

For long-running/multi-conversation projects, establish/update root `CURRENT.md` after current authority/design/task state is understood. It records only NOW and points to `reports/design/...` owners.

Do not create CURRENT for trivial single-session projects merely for symmetry.

## Delta migration

Typical migration surfaces are:

```text
AGENTS.md
CURRENT.md
root design/ → reports/design/
reports/ governance/report layout
project Skill/references
shared coding-Skill coordinates when used
Actions/verification placement when implicated
local tmp/worktree policy when stale
```

Already-conforming files are not rewritten for style alone.

## Execution placement

Repository-only migration that connected ChatGPT can safely complete is DIRECT. Use Codex only for genuine local filesystem/runtime/environment evidence.

## Completion

Migration is complete when:

```text
project AGENTS routes current authority correctly
AND CURRENT is correct/omitted deliberately
AND current design exists as one reports/design/ tree when explicit design is used
AND reports/concept remains history/input only
AND Skill/references project current design
AND duplicate/parallel authority surfaces are removed/demoted
AND active task/report/blocker state is reconciled
AND future conversation replacement uses normal resume rather than rerunning migration
```
