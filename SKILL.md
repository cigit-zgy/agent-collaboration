---
name: agent-collaboration
description: >
  Coordinate User, ChatGPT, and Codex for repository work involving design, direct remote action,
  AI-assisted implementation, local execution, verification, acceptance review, project integration,
  or Skill maintenance.
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
+ formal task author when needed
+ acceptance reviewer

Codex
= LOCAL implementation/execution agent
= does not self-accept

project tooling / CI
= mechanical style and verification evidence
```

Deliverables are partitioned by capability:

```text
DIRECT → ChatGPT completes with connected capability
LOCAL  → Codex executes locally when local/runtime capability is materially required
```

Repository mutation alone does not make a deliverable LOCAL.

For executable implementation quality and AI-code transparency, read `references/collaboration/implementation.md`.

## Execution routes

Use the lightest route that preserves the required trust/evidence:

```text
DIRECT
→ ChatGPT completes + verifies

LOCAL-QUICK
→ bounded low-risk local change/execution
→ concise Codex instruction
→ focused verification + commit/push when needed
→ ChatGPT acceptance review

FORMAL
→ major/long/risk-sensitive/release/trust/public-contract work
→ committed task on a dedicated task branch by default
→ Codex implementation + required evidence + report
→ ChatGPT acceptance review
→ integration
```

Detailed routing, Git safety, authority resolution, instruction/data trust boundary, concurrency, ownership boundaries, and acceptance live in `references/collaboration/protocol.md`.

## Reference routing

### Collaboration

- `references/collaboration/protocol.md` — roles, authority, DIRECT/LOCAL partition, DIRECT/LOCAL-QUICK/FORMAL routes, Git/task-branch workflow, trust boundaries, concurrency, acceptance;
- `references/collaboration/implementation.md` — AI-assisted implementation transparency, reviewability, engineering discipline, code-quality expectations;
- `references/collaboration/verification.md` — verification levels, evidence categories, risk-based tools and strengthening techniques;
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

- `repository.md` — canonical source modes, discovery, distribution, source resolution;
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
small local implementation → protocol.md + implementation.md
formal release task         → protocol.md + implementation.md + verification.md + task template
project redesign            → target project design authority + project/concept.md
```

Do not preload the whole collaboration repository.

## Completion

Collaboration work is complete when the selected route has completed all DIRECT and LOCAL deliverables, required evidence exists, material limitations are disclosed, and the applicable ChatGPT acceptance review/human decision gate is satisfied.
