---
name: agent-collaboration
description: >
  Coordinate User, ChatGPT, and Codex for repository work involving design, direct remote action,
  AI-assisted implementation, shared coding-Skill alignment, local execution, verification,
  acceptance review, project integration, conversation handoff/context recovery, or Skill maintenance.
---

# Agent Collaboration

## Purpose

This Skill routes the collaboration contract for:

```text
User ↔ ChatGPT ↔ Codex
```

Canonical maintained source:

```text
GitHub repository: cigit-zgy/agent-collaboration
```

Do not rely on remembered collaboration policy across unrelated repository-changing work. At the first substantive write of a new ChatGPT work unit, verify current `agent-collaboration` authority once; FORMAL tasks then pin that exact commit. Codex uses the task pin for FORMAL work and refreshes current authority once at the start of a new unpinned LOCAL repository task/session. See `references/collaboration/protocol.md`.

Formal delegated tasks pin the exact collaboration commit they use. No machine-local installation is assumed; a verified local checkout at the same repository/commit is only a cache.

Load only the reference that owns the active concern.

## Core operating model

```text
User
= goals + genuine scientific/product/design/tool decisions
= final decision/override authority
= may use a zero-human-coding workflow

ChatGPT
= design partner
+ connected DIRECT executor
+ primary author of code/tests it can correctly write from repository context and shared Skills
+ primary author of project conversation handoffs
+ formal task author when local execution/verification remains
+ acceptance reviewer

Codex
= LOCAL implementation/execution agent
= local verification, debugging, and bounded repair
= primary code author only when implementation materially requires a local feedback loop
= may use current handoff as background when routed there, but does not treat it as authority
= does not self-accept

project tooling / CI
= mechanical style and verification evidence
```

Deliverables are partitioned by capability, and implementation authorship is separated from verification placement:

```text
ChatGPT-authorable code/tests
→ ChatGPT writes first

cheap checks already supported online
→ ChatGPT verifies

environment-bound or time-consuming checks
→ Codex verifies locally and repairs when required
```

Repository mutation or later local verification alone does not make the original authoring deliverable LOCAL.

For executable implementation quality and AI-code transparency, read `references/collaboration/implementation.md`.

For shared third-party coding-Skill authority and local alignment, read `references/collaboration/shared-coding-skills.md`.

For new project/core design or major redesign, complete the mandatory external prior-art/reuse gate in `references/project/prior-art.md` before freezing a concept or starting substantial custom implementation.

For conversation migration or context recovery in an existing project, use `references/project/handoff.md`.

## Execution routes

Use the lightest route that preserves the required trust/evidence:

```text
DIRECT
→ ChatGPT completes authoring and supported verification

LOCAL-QUICK
→ bounded low-risk local verification/repair or implementation
→ concise Codex instruction
→ project-local tmp scratch boundary when needed
→ focused verification + cleanup + commit/push when needed
→ ChatGPT acceptance review

FORMAL
→ major/long/risk-sensitive/release/trust/public-contract work
→ committed task on a dedicated task branch by default
→ local scratch/worktree state under <PROJECT_ROOT>/tmp/<TASK_ID>/ by default
→ Codex local implementation and/or remaining verification + report
→ cleanup or explicit retained-recovery state
→ ChatGPT acceptance review
→ integration
```

Detailed routing, Git safety, authority refresh, project-local temporary-state boundary, instruction/data trust boundary, concurrency, ownership boundaries, report lookup, and acceptance live in `references/collaboration/protocol.md`.

## Reference routing

### Collaboration

- `references/collaboration/protocol.md` — roles, authority refresh, DIRECT/LOCAL partition, DIRECT/LOCAL-QUICK/FORMAL routes, local tmp boundary, Git/task-branch workflow, trust boundaries, concurrency, report lookup, integration, acceptance;
- `references/collaboration/implementation.md` — ChatGPT-first code authoring, prior-art reuse enforcement, AI-assisted implementation transparency, reviewability, engineering discipline, code-quality expectations;
- `references/collaboration/shared-coding-skills.md` — immutable cross-Agent coding-Skill profile, precedence, activation, local alignment, update policy;
- `references/collaboration/verification.md` — verification levels, evidence categories, online/local placement, risk-based tools and strengthening techniques;
- `references/collaboration/agents.md` — maintained `AGENTS.md` writing standard;
- `references/collaboration/templates/` — formal ChatGPT task and Codex report formats.

### Project

Use `references/project/` when a scientific/software project joins the collaboration:

- `architecture.md` — project entry, responsibility-based ownership, report families, and project-local `tmp/` ephemeral boundary;
- `concept.md` — project `reports/concept/` design-authority lifecycle and prior-art freeze gate;
- `prior-art.md` — mandatory literature↔open-source search, candidate inspection, reuse/adapt/reject decision, and concept-recording contract for substantial new design;
- `handoff.md` — conversation migration artifact, `reports/handoff/README.md` current-pointer index, handoff metadata/body, and fast context-recovery route;
- `templates/agents.md` — project root `AGENTS.md` specialization;
- `templates/skill.md` — project workflow `SKILL.md`.

### Skill

Use `references/skill/` for Skill ownership/package/writing:

- `repository.md` — canonical source modes, discovery, distribution, cross-Agent authority resolution;
- `package.md` — package resources, profiles, runtime/environment ownership;
- `writing.md` — maintained `SKILL.md` and `references/*.md` writing standard;
- `templates/agents.md` — maintained first-party Skill-repository `AGENTS.md` specialization.

## Progressive disclosure

Ordinary route:

```text
applicable AGENTS.md
→ this SKILL.md
→ one owning reference
→ only additional owner needed by the active concern
```

Examples:

```text
ChatGPT authors ordinary code
→ implementation.md + activated entries from shared-coding-skills.md

local verification/repair
→ protocol.md + implementation.md + verification.md + activated Skill authorities

formal release task
→ protocol.md + implementation.md + shared-coding-skills.md + verification.md + task template

new project / major new design
→ project/prior-art.md
→ strongest external literature/open-source precedents
→ target project concept authority
→ project/concept.md

conversation migration
→ project/handoff.md
→ create reports/handoff/<handoff>.md + update reports/handoff/README.md

new conversation/context recovery
→ project AGENTS.md
→ reports/handoff/README.md
→ current handoff only
→ current project/collaboration authorities

routine project redesign without a new major design concern
→ target project design authority + project/concept.md
```

Do not preload the whole collaboration repository, every installed Skill, or every historical handoff for ordinary work.

## Completion

Collaboration work is complete when the selected route has completed all authoring and LOCAL execution deliverables, any applicable prior-art gate is complete and respected, ChatGPT and Codex used the same applicable shared coding-Skill authorities, Agent-created local temporary state is cleaned or explicitly retained for a concrete recovery reason, required evidence exists, material limitations are disclosed, and the applicable ChatGPT acceptance review/human decision gate is satisfied.

A conversation migration is complete when the new committed handoff is substantially self-contained, `reports/handoff/README.md` points to it, source/evidence pointers are recoverable, and the next context can resume by reconciling the handoff against current authority rather than rereading the entire prior conversation.
