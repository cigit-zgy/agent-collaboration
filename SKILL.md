---
name: agent-collaboration
description: >
  Coordinate User, ChatGPT, and Codex for repository work involving project or Skill design,
  prior-art research, direct authoring, local execution, verification, GitHub Actions, FORMAL
  delegation/acceptance, shared coding-Skill alignment, project integration, conversation
  handoff/context recovery, or Skill maintenance.
---

# Agent Collaboration

Canonical maintained source:

```text
cigit-zgy/agent-collaboration
```

This file is the **sole runtime routing index** for collaboration policy. Read only the owner(s) selected for the active concern; do not preload the repository.

## Minimal operating model

```text
User
= goals + genuine scientific/product/design/tool decisions
= final decision/override authority

ChatGPT
= design partner
= connected DIRECT author/executor
= primary author of code/tests it can correctly produce
= primary conversation-handoff author
= FORMAL task author
= acceptance reviewer

Codex
= LOCAL implementation/execution agent
= environment-bound verification/debugging/bounded repair
= primary code author only when correctness materially needs a local feedback loop
= does not self-accept
```

At the first substantive write of a new repository-changing ChatGPT work unit, verify current collaboration authority once. FORMAL tasks pin that exact commit. Codex uses the task pin for FORMAL work and refreshes current authority once at the start of a new unpinned local repository task/session.

## Direct routing table

Normal route depth is:

```text
SKILL.md → owning reference
```

Use at most one primary owner plus one explicitly necessary secondary owner. Do not follow mandatory reference chains.

| Active concern | Primary owner | Also read only when needed |
|---|---|---|
| roles, authority, refresh, instruction/data trust, unresolved design | `references/collaboration/protocol.md` | none |
| DIRECT / LOCAL-QUICK / FORMAL route selection, local Git/worktree/tmp/concurrency | `references/collaboration/execution.md` | `formal.md` only when FORMAL lifecycle is needed |
| FORMAL task/report binding, handoff, acceptance, report lookup, integration | `references/collaboration/formal.md` | exact task/report template being created/reviewed |
| executable implementation quality, ChatGPT-first authoring, engineering discipline | `references/collaboration/implementation.md` | `verification.md` when evidence planning is also required |
| verification level, evidence categories, ChatGPT-vs-Codex placement | `references/collaboration/verification.md` | none |
| GitHub Actions / CI design, private/public defaults, claim deduplication, budget | `references/collaboration/actions.md` | `verification.md` only when verification level/evidence design is also needed |
| shared coding-Skill authority/alignment | `references/collaboration/shared-coding-skills.md` | none |
| author/review `AGENTS.md` | `references/collaboration/agents.md` | relevant project/Skill AGENTS template |
| project ownership/integration/report-family placement | `references/project/architecture.md` | none |
| external CLI/API/schema/parser/simulator adapter/profile/reproducibility | `references/project/external-tools.md` | none |
| project concept authority/freeze/reopen/projection | `references/project/concept.md` | none |
| new project/core design or major architecture/tool choice | `references/project/prior-art.md` | target project concept authority |
| conversation migration/recovery semantics | `references/project/handoff.md` | `references/project/templates/handoff.md` only when authoring a new handoff |
| maintained first-party Skill design, implementation, testing lifecycle | `references/skill/development.md` | target concept/design authority when declared |
| Skill Markdown/reference writing quality | `references/skill/writing.md` | `development.md` only when behavior/design is changing |
| Skill maintained source/discovery/distribution | `references/skill/repository.md` | none |
| Skill package/resources/runtime ownership | `references/skill/package.md` | none |

## High-frequency routes

### Ordinary implementation

```text
project AGENTS.md
→ collaboration/implementation.md
→ activated coding Skill(s)
→ verification.md only if evidence planning is needed
```

Do not load FORMAL, prior-art, handoff, Actions, or history merely because code is being changed.

### Skill design or Skill testing

```text
target concept/design authority
→ skill/development.md
→ target SKILL.md / relevant target reference
```

Testing primarily probes general Skill design/contract insufficiency. If tests expose a `DESIGN_GAP`, return to concept/design and Skill Markdown before code repair. Do not optimize production code around one task fixture.

Load `skill/writing.md` only when editing/reviewing Skill Markdown structure or language.

### New project / major new design

```text
project/prior-art.md
→ strongest authoritative literature/open-source precedents
→ target project concept authority
```

Do not begin substantial custom implementation before the applicable prior-art/reuse decision is durable.

### LOCAL execution

```text
collaboration/execution.md
→ project/local runtime
```

Agent-created persistent local scratch belongs under the target project `tmp/` boundary. Do not create sibling project worktrees for convenience.

### FORMAL delegation

```text
collaboration/formal.md
+ collaboration/execution.md when local Git/worktree mechanics matter
+ verification.md only for the required evidence plan
+ templates/chatgpt-task.md only while creating/reviewing the task
```

The committed task is the sole task-specific execution specification. User-visible Codex launch text is emitted in a fenced `text` code block with a Copy control.

### FORMAL completion

```text
collaboration/formal.md
+ expected Codex report
+ templates/codex-report.md only when validating report format
```

A short User message such as `Codex 已完成` is enough when the active context resolves the latest relevant FORMAL task.

### GitHub Actions review

```text
collaboration/actions.md
```

Add `verification.md` only when the task also asks which verification level/evidence categories are needed. Do not duplicate a Codex-proven claim in Actions without a distinct hosted-environment reason.

### Conversation migration

Authoring:

```text
project/handoff.md
+ project/templates/handoff.md
```

Recovery:

```text
project AGENTS.md
→ reports/handoff/README.md
→ current handoff only
→ current project/collaboration authority + repository state
```

Do not preload old handoffs.

## Cold-path discipline

Do not preload these merely because they exist:

```text
references/**/templates/       unless creating/reviewing that artifact
reports/concept/               collaboration decision history
reports/chatgpt/               except the active FORMAL task
reports/codex/                 except the active expected report
older reports/handoff/         except explicit historical reconstruction
README.md                      human orientation, not runtime policy
```

Historical collaboration concepts are rationale/history; current operational authority lives in `references/` and applicable `AGENTS.md` / `SKILL.md` files.

## Context-efficiency target

The normal collaboration read set is:

```text
this thin router
+ one primary owning reference
+ zero or one necessary secondary owner
```

If an Agent must read several large collaboration files before discovering the correct owner, treat that as a routing/design defect.

## Completion

Collaboration work is complete when the selected route has satisfied its durable design/implementation/execution/evidence requirements, material limitations are disclosed, temporary local state is cleaned or deliberately retained for recovery, and the applicable ChatGPT acceptance/User checkpoint is satisfied.
