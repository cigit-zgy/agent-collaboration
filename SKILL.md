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

This file is the sole runtime routing index. Read only the owner(s) selected for the active concern; do not preload the repository.

## Operating model

```text
User    = goals + genuine scientific/product/design/tool decisions + final override
ChatGPT = design partner + connected author/executor + durable Codex-task author + acceptance reviewer
Codex   = LOCAL implementation/execution + environment-bound verification/repair; never self-accepts
```

At the first substantive write of a new repository-changing ChatGPT work unit, verify current collaboration authority once. Delegated Codex tasks pin the applicable collaboration revision in their committed task artifact.

## Direct routing

Normal route depth:

```text
SKILL.md → owning reference
```

Use one primary owner plus at most one explicitly necessary secondary owner.

| Active concern | Primary owner | Secondary only when needed |
|---|---|---|
| roles, authority, refresh, instruction/data trust, unresolved design | `references/collaboration/protocol.md` | none |
| DIRECT/LOCAL-QUICK/FORMAL route selection, remote sync, local Git/worktree/tmp/concurrency | `references/collaboration/execution.md` | exact LOCAL-QUICK task template when delegating |
| FORMAL task/report binding, acceptance, report lookup, integration | `references/collaboration/formal.md` | exact FORMAL task/report template when creating/reviewing |
| executable implementation quality, ChatGPT-first authoring, engineering discipline | `references/collaboration/implementation.md` | `verification.md` for evidence planning |
| verification level, evidence categories, ChatGPT-vs-Codex placement | `references/collaboration/verification.md` | none |
| GitHub Actions/CI design, private/public defaults, claim deduplication, budget | `references/collaboration/actions.md` | `verification.md` for level/evidence design |
| shared coding-Skill authority/alignment | `references/collaboration/shared-coding-skills.md` | none |
| author/review `AGENTS.md` | `references/collaboration/agents.md` | relevant project/Skill AGENTS template |
| project ownership/integration architecture | `references/project/architecture.md` | none |
| normal multi-conversation resume / root `CURRENT.md` | `references/project/current.md` | `references/project/templates/current.md` only when creating/restructuring CURRENT |
| migrate an existing project to current collaboration policy/architecture | `references/project/migration.md` | migration bootstrap template only when a new conversation needs it |
| reports layout, naming/metadata, archive placement, report cleanup | `references/project/reports.md` | family-specific owner/template only when needed |
| chronological design exploration/history in `reports/concept/` | `references/project/concept.md` | concept template only when authoring a concept note |
| current canonical project design under `design/` | `references/project/design.md` | design template only when creating/restructuring living design |
| external CLI/API/schema/parser/simulator adapter/profile/reproducibility | `references/project/external-tools.md` | none |
| new project/core design or major architecture/tool choice | `references/project/prior-art.md` | current target `design/` topic(s) after adjudication |
| exceptional conversation-only continuity not representable elsewhere | `references/project/handoff.md` | handoff template only when authoring the exceptional delta artifact |
| maintained first-party Skill design/implementation/testing lifecycle | `references/skill/development.md` | current target `design/` authority when declared |
| Skill Markdown/reference writing quality | `references/skill/writing.md` | `development.md` when behavior/design is changing |
| Skill maintained source/discovery/distribution | `references/skill/repository.md` | none |
| Skill package/resources/runtime ownership | `references/skill/package.md` | none |

## Hard routing rules

### Normal conversation resume — repository carries continuity

Replacing a full conversation in an already-integrated project is **not** project migration and normally does **not** require a handoff.

For projects using the current-work-state contract:

```text
old conversation
→ make accepted durable state belong to its real repository owner
→ rewrite root CURRENT.md to the actual work edge
→ create handoff only for unavoidable residual conversation-only delta
→ end

new conversation
→ AGENTS.md
→ CURRENT.md
→ design/README.md when present
→ load only the current concern just in time
```

When the User says something equivalent to `换对话框，给我提示词`, route to `project/current.md` and return only its canonical compact resume prompt for the active repository. Do not explain migration/handoff/current-state architecture unless explicitly asked.

`CURRENT.md` records only NOW; it is not a history log. Do not preload the full design tree, concept history, old task/report files, old handoffs, archive, or collaboration reference tree merely to resume.

Before the first substantive repository-changing write, refresh current collaboration authority once under `protocol.md`; this does not justify loading unrelated collaboration owners during orientation.

### Codex delegation — task body never lives in chat

Every repository task delegated to Codex uses:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

before the handoff occurs.

```text
LOCAL-QUICK
→ committed ChatGPT task
→ very short copyable locator
→ compact Result contract only
→ no reports/codex artifact

FORMAL
→ committed ChatGPT task
→ very short copyable locator
→ bound reports/codex artifact
→ acceptance / integration lifecycle
```

The committed task is the sole task-specific execution specification. Chat MUST NOT repeat the detailed task as a long prompt.

### Codex remote synchronization — hard boundary

Every repository-changing Codex task executes against the latest authorized fetched remote state.

Before repository mutation:

```text
fresh fetch
→ resolve exact committed task + authorized remote baseline
→ inspect local branch/HEAD/upstream/worktrees/User state
→ establish safe task branch/worktree
→ prove local execution HEAD == authorized fetched remote baseline
```

After repository mutation:

```text
commit task-scoped changes
→ push owning branch
→ fresh fetch again
→ prove local task HEAD == fetched upstream HEAD
→ only then report PASS/completion
```

Synchronization does not authorize blind `git pull`, reset, rebase, stash, force checkout, or force push.

### Existing-project migration

Project-policy migration changes repository architecture/policy; it is not routine conversation resume.

```text
project/migration.md
→ current target repository state
→ only directly relevant current owners/history
→ delta migration
```

Do not reconstruct the old conversation. When migration establishes a long-running multi-conversation project, create/update `CURRENT.md` as the current work pointer rather than using a handoff as normal state.

### Project design model

```text
reports/concept/
= what we considered / historical design thinking

design/
= what we currently accept / one canonical living design set

CURRENT.md
= what we are working on now / current execution-work pointer
```

A material new idea changes project authority only after User + ChatGPT adjudication updates `design/` into one coherent current state.

### Skill behavior changes

```text
current accepted design/
→ target SKILL.md + references
→ implementation
→ design-probing tests
```

Use `skill/development.md`. If tests expose `DESIGN_GAP`, return to design adjudication and Skill Markdown before code repair.

### New project / major design

Use `project/prior-art.md` before accepting a major custom design into `design/`.

### Reports / archive

Use `project/reports.md`. If `reports/` exists, its active surface is limited to `chatgpt/`, `codex/`, `concept/`, and `handoff/`. `CURRENT.md` is a root current-state owner, not a report family. Historical retention uses the single repository-root `00_archive/`.

### Exceptional handoff

`reports/handoff/` is not the default resume mechanism. Use it only when meaningful conversation-only continuity cannot reasonably be represented in AGENTS/design/CURRENT/task/report/concept or another real owner. No handoff is preferable to a redundant handoff.

## Cold paths

Do not preload:

```text
references/**/templates/   unless creating/reviewing that artifact
reports/concept/           except active design-history/adjudication work
reports/chatgpt/           except the active delegated task
reports/codex/             except the expected active FORMAL report
reports/handoff/           except explicit exceptional continuity recovery
00_archive/                historical only
README.md                   human orientation only
```

For normal conversation resume, the project-text orientation set is `AGENTS.md + CURRENT.md + design/README.md` when those files exist. Then read only directly relevant owners.

## Context target

```text
orientation
= project AGENTS.md + CURRENT.md + design/README.md

active work
= one primary owner + zero/one necessary secondary owner

historical preload
= zero
```

A mature project should normally identify the current concern before loading roughly 10–12 KiB of project text; exceeding ~16 KiB before useful work starts is a routing smell, not a reason to enlarge the handoff.

## Completion

Work is complete when the selected route satisfies its durable design/implementation/execution/evidence requirements, CURRENT reflects the adopted current work edge when the project uses it, material limitations are disclosed, remote synchronization evidence is complete for repository-changing Codex work, temporary local state is cleaned or deliberately retained for recovery, and the applicable ChatGPT acceptance/User checkpoint is satisfied.
