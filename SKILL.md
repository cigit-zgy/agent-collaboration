---
name: agent-collaboration
description: >
  Coordinate User, ChatGPT, and Codex for repository work involving project or Skill design,
  prior-art research, direct authoring, local execution, verification, GitHub Actions, FORMAL
  delegation/acceptance, shared coding-Skill alignment, project integration, conversation
  handoff/context recovery, report/archive governance, or Skill maintenance.
---

# Agent Collaboration

Canonical source: `cigit-zgy/agent-collaboration`.

This file is the **sole runtime routing index**. Read only the owner(s) selected for the active concern; do not preload the repository.

## Operating model

```text
User    = goals + genuine scientific/product/design/tool decisions + final override
ChatGPT = design partner + connected author/executor + FORMAL task author + acceptance reviewer
Codex   = LOCAL implementation/execution + environment-bound verification/repair; never self-accepts
```

At the first substantive write of a new repository-changing ChatGPT work unit, verify current collaboration authority once. FORMAL tasks pin that exact commit. Codex uses the task pin for FORMAL work and refreshes current authority once at the start of a new unpinned local repository task/session.

## Direct routing

Normal route depth:

```text
SKILL.md → owning reference
```

Use one primary owner plus at most one explicitly necessary secondary owner. Avoid mandatory reference chains.

| Active concern | Primary owner | Secondary only when needed |
|---|---|---|
| roles, authority, refresh, instruction/data trust, unresolved design | `references/collaboration/protocol.md` | none |
| DIRECT/LOCAL-QUICK/FORMAL route selection, local Git/worktree/tmp/concurrency | `references/collaboration/execution.md` | `formal.md` for FORMAL lifecycle |
| FORMAL task/report binding, handoff, acceptance, report lookup, integration | `references/collaboration/formal.md` | exact task/report template being created/reviewed |
| executable implementation quality, ChatGPT-first authoring, engineering discipline | `references/collaboration/implementation.md` | `verification.md` for evidence planning |
| verification level, evidence categories, ChatGPT-vs-Codex placement | `references/collaboration/verification.md` | none |
| GitHub Actions/CI design, private/public defaults, claim deduplication, budget | `references/collaboration/actions.md` | `verification.md` for level/evidence design |
| shared coding-Skill authority/alignment | `references/collaboration/shared-coding-skills.md` | none |
| author/review `AGENTS.md` | `references/collaboration/agents.md` | relevant project/Skill AGENTS template |
| project ownership/integration architecture | `references/project/architecture.md` | none |
| reports layout, naming/metadata, archive placement, report cleanup | `references/project/reports.md` | family-specific owner/template only when needed |
| chronological design exploration/history in `reports/concept/` | `references/project/concept.md` | `references/project/templates/concept.md` only when authoring a concept note |
| current canonical project design under `design/`, dynamic topic decomposition | `references/project/design.md` | `references/project/templates/design.md` only when creating/restructuring living design |
| external CLI/API/schema/parser/simulator adapter/profile/reproducibility | `references/project/external-tools.md` | none |
| new project/core design or major architecture/tool choice | `references/project/prior-art.md` | current target `design/` topic(s) after adjudication |
| conversation migration/recovery semantics | `references/project/handoff.md` | `references/project/templates/handoff.md` only when authoring a new handoff |
| maintained first-party Skill design/implementation/testing lifecycle | `references/skill/development.md` | current target `design/` authority when declared |
| Skill Markdown/reference writing quality | `references/skill/writing.md` | `development.md` when behavior/design is changing |
| Skill maintained source/discovery/distribution | `references/skill/repository.md` | none |
| Skill package/resources/runtime ownership | `references/skill/package.md` | none |

## Hard routing rules

### Project design model

```text
reports/concept/
= what we considered / historical design thinking

design/
= what we currently accept / one canonical living design set
```

A material new idea may create a dated concept note. It changes project authority only after User + ChatGPT adjudication updates `design/` into one coherent current state.

Do not keep old/draft/versioned design copies under `design/`. Use `project/design.md` for dynamic add/update/split/merge/remove/reorder rules.

### Skill behavior changes

```text
current accepted design/
→ target SKILL.md + references
→ implementation
→ design-probing tests
```

Use `skill/development.md`. If tests expose `DESIGN_GAP`, return to design adjudication and Skill Markdown before code repair. Do not optimize production code around one task fixture.

### New project / major design

Use `project/prior-art.md` before accepting a major custom design into `design/`. Substantial custom implementation begins only after the reuse/adapt/custom-gap decision is durable in the current living design.

### Reports / archive

Use `project/reports.md`. If `reports/` exists, its active surface is limited to `chatgpt/`, `codex/`, `concept/`, and `handoff/`; every report Markdown file follows the canonical dated family filename and required YAML metadata. Historical retention uses the single repository-root `00_archive/`, never `archive/` or nested `00_archive/`.

`reports/concept/` is design history/input, not current design authority.

### FORMAL work

Use `formal.md`; add `execution.md` only for local Git/worktree mechanics and `verification.md` only for required evidence design. Load the exact task/report template only while creating/reviewing that artifact.

The committed task is the sole task-specific execution specification. User-visible Codex launch text is a fenced `text` block with a Copy control.

### Conversation migration

Authoring reads `project/handoff.md` + `project/templates/handoff.md`.

Recovery reads:

```text
project AGENTS.md
→ newest valid reports/handoff/YYMMDD_handoff_NN.md
→ current authority + repository state
```

Do not preload older handoffs.

## Cold paths

Do not preload:

```text
references/**/templates/   unless creating/reviewing that artifact
reports/concept/           except active design-history/adjudication work
reports/chatgpt/           except active FORMAL task
reports/codex/             except expected active report
older reports/handoff/     except explicit historical reconstruction
00_archive/                historical only
README.md                   human orientation only
```

For current design, read `design/README.md` and only the directly relevant topic files; do not preload the entire design tree for a bounded concern.

## Context target

Normal collaboration context is:

```text
this router
+ one primary owner
+ zero or one necessary secondary owner
+ zero historical preload
```

If an Agent must read several large collaboration files before discovering the correct owner, treat that as a routing/design defect.

## Completion

Work is complete when the selected route satisfies its durable design/implementation/execution/evidence requirements, material limitations are disclosed, temporary local state is cleaned or deliberately retained for recovery, and the applicable ChatGPT acceptance/User checkpoint is satisfied.
