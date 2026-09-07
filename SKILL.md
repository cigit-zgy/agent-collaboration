---
name: agent-collaboration
description: >
  Coordinate User, ChatGPT, and Codex for repository work involving project or Skill design,
  prior-art research, existing-project migration, direct authoring, local execution, verification,
  GitHub Actions, Codex delegation/acceptance, shared coding-Skill alignment, project integration,
  conversation handoff/context recovery, report/archive governance, or Skill maintenance.
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
| DIRECT/LOCAL-QUICK/FORMAL route selection, local Git/worktree/tmp/concurrency | `references/collaboration/execution.md` | exact LOCAL-QUICK task template when delegating |
| FORMAL task/report binding, acceptance, report lookup, integration | `references/collaboration/formal.md` | exact FORMAL task/report template when creating/reviewing |
| executable implementation quality, ChatGPT-first authoring, engineering discipline | `references/collaboration/implementation.md` | `verification.md` for evidence planning |
| verification level, evidence categories, ChatGPT-vs-Codex placement | `references/collaboration/verification.md` | none |
| GitHub Actions/CI design, private/public defaults, claim deduplication, budget | `references/collaboration/actions.md` | `verification.md` for level/evidence design |
| shared coding-Skill authority/alignment | `references/collaboration/shared-coding-skills.md` | none |
| author/review `AGENTS.md` | `references/collaboration/agents.md` | relevant project/Skill AGENTS template |
| project ownership/integration architecture | `references/project/architecture.md` | none |
| migrate an existing project to current collaboration policy/architecture | `references/project/migration.md` | migration bootstrap template only when a new conversation needs it |
| reports layout, naming/metadata, archive placement, report cleanup | `references/project/reports.md` | family-specific owner/template only when needed |
| chronological design exploration/history in `reports/concept/` | `references/project/concept.md` | concept template only when authoring a concept note |
| current canonical project design under `design/` | `references/project/design.md` | design template only when creating/restructuring living design |
| external CLI/API/schema/parser/simulator adapter/profile/reproducibility | `references/project/external-tools.md` | none |
| new project/core design or major architecture/tool choice | `references/project/prior-art.md` | current target `design/` topic(s) after adjudication |
| conversation migration/recovery semantics | `references/project/handoff.md` | handoff template only when authoring a new handoff |
| maintained first-party Skill design/implementation/testing lifecycle | `references/skill/development.md` | current target `design/` authority when declared |
| Skill Markdown/reference writing quality | `references/skill/writing.md` | `development.md` when behavior/design is changing |
| Skill maintained source/discovery/distribution | `references/skill/repository.md` | none |
| Skill package/resources/runtime ownership | `references/skill/package.md` | none |

## Hard routing rules

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

If the task cannot be committed/pushed, do not fall back to a chat-only long instruction; report the blocker.

### Existing-project migration

Project-policy migration is not a request to reread the old conversation.

```text
old conversation
→ make important non-repository state durable when possible
→ emit short migration bootstrap only if a new conversation is taking over

new/current conversation
→ project/migration.md
→ current target repository state
→ only directly relevant current owners/history
→ delta migration
```

Do not preload all concept notes, Codex reports, handoffs, or collaboration references.

### Project design model

```text
reports/concept/
= what we considered / historical design thinking

design/
= what we currently accept / one canonical living design set
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

Use `project/reports.md`. If `reports/` exists, its active surface is limited to `chatgpt/`, `codex/`, `concept/`, and `handoff/`. Historical retention uses the single repository-root `00_archive/`.

### Conversation migration

Authoring reads `project/handoff.md` + its template. Recovery reads only the newest valid handoff plus current authority/state.

## Cold paths

Do not preload:

```text
references/**/templates/   unless creating/reviewing that artifact
reports/concept/           except active design-history/adjudication work
reports/chatgpt/           except the active delegated task
reports/codex/             except the expected active FORMAL report
older reports/handoff/     except explicit historical reconstruction
00_archive/                historical only
README.md                   human orientation only
```

For current design, read `design/README.md` and only directly relevant topic files.

## Context target

```text
this router
+ one primary owner
+ zero or one necessary secondary owner
+ active task artifact only when delegation is occurring
+ zero historical preload
```

If an Agent must read several large files before discovering the correct owner, treat that as a routing/design defect.

## Completion

Work is complete when the selected route satisfies its durable design/implementation/execution/evidence requirements, material limitations are disclosed, temporary local state is cleaned or deliberately retained for recovery, and the applicable ChatGPT acceptance/User checkpoint is satisfied.
