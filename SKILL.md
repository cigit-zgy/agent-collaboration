---
name: agent-collaboration
description: >
  Coordinate User, ChatGPT, and Codex for repository work involving design, direct remote action,
  AI-assisted implementation, shared coding-Skill alignment, local execution, verification,
  acceptance review, project integration, or Skill maintenance.
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
+ formal task author when local execution/verification remains
+ acceptance reviewer

Codex
= LOCAL implementation/execution agent
= local verification, debugging, and bounded repair
= primary code author only when implementation materially requires a local feedback loop
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

## Execution routes

Use the lightest route that preserves the required trust/evidence:

```text
DIRECT
→ ChatGPT completes authoring and supported verification

LOCAL-QUICK
→ bounded low-risk local verification/repair or implementation
→ concise Codex instruction
→ focused verification + commit/push when needed
→ ChatGPT acceptance review

FORMAL
→ major/long/risk-sensitive/release/trust/public-contract work
→ committed task on a dedicated task branch by default
→ Codex local implementation and/or remaining verification + report
→ ChatGPT acceptance review
→ integration
```

Detailed routing, Git safety, authority resolution, instruction/data trust boundary, concurrency, ownership boundaries, report lookup, and acceptance live in `references/collaboration/protocol.md`.

## Reference routing

### Collaboration

- `references/collaboration/protocol.md` — roles, authority, DIRECT/LOCAL partition, DIRECT/LOCAL-QUICK/FORMAL routes, Git/task-branch workflow, trust boundaries, concurrency, report lookup, integration, acceptance;
- `references/collaboration/implementation.md` — ChatGPT-first code authoring, AI-assisted implementation transparency, reviewability, engineering discipline, code-quality expectations;
- `references/collaboration/shared-coding-skills.md` — immutable cross-Agent coding-Skill profile, precedence, activation, local alignment, update policy;
- `references/collaboration/verification.md` — verification levels, evidence categories, online/local placement, risk-based tools and strengthening techniques;
- `references/collaboration/agents.md` — maintained `AGENTS.md` writing standard;
- `references/collaboration/templates/` — formal ChatGPT task and Codex report formats.

### Project

Use `references/project/` when a scientific/software project joins the collaboration:

- `architecture.md` — project entry and responsibility-based ownership;
- `concept.md` — project `reports/concept/` design-authority lifecycle;
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

project redesign
→ target project design authority + project/concept.md
```

Do not preload the whole collaboration repository or every installed Skill.

## Completion

Collaboration work is complete when the selected route has completed all authoring and LOCAL execution deliverables, ChatGPT and Codex used the same applicable shared coding-Skill authorities, required evidence exists, material limitations are disclosed, and the applicable ChatGPT acceptance review/human decision gate is satisfied.
