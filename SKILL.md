---
name: agent-collaboration
description: >
  Coordinate User, ChatGPT, and Codex for repository work involving design, direct remote action,
  local execution, verification, acceptance review, project integration, or Skill maintenance.
---

# Agent Collaboration

## Purpose

This Skill routes the collaboration contract for:

```text
User ↔ ChatGPT ↔ Codex
```

Load only the reference family that owns the active concern.

## Core route

For design, delegation, local execution mode selection, Git synchronization, concurrency, verification, and acceptance review, read:

```text
references/collaboration/protocol.md
```

The stable role split is:

```text
User            = goals, genuine human decisions, final decision/override authority
User + ChatGPT  = design collaboration
ChatGPT         = direct executor when connected capabilities suffice
                  + independent technical acceptance reviewer
Codex           = local executor when genuinely local/unavailable capability is required
```

Codex does not self-accept.

## Reference routing

### Collaboration

Use `references/collaboration/` for the three-party operating loop:

- `protocol.md` — roles, routine-vs-formal Codex execution, Git synchronization, concurrency, acceptance;
- `verification.md` — verification levels and risk-based tool selection;
- `agents.md` — collaboration-wide `AGENTS.md` writing standard;
- `templates/` — formal ChatGPT task/launch format and Codex report format.

### Project

Use `references/project/` when a scientific/software project joins this collaboration:

- `architecture.md` — project entry and responsibility-based ownership patterns;
- `concept.md` — `reports/concept/` design-authority contract, concept writing standard, and review/adjudication/freeze/projection lifecycle;
- `templates/agents.md` — project root `AGENTS.md` specialization;
- `templates/skill.md` — project workflow `SKILL.md`.

### Skill

Use `references/skill/` for first-party/third-party Skill ownership and package design:

- `repository.md` — maintained source, discovery, distribution, rename lifecycle;
- `package.md` — package resources, profiles, runtime/environment ownership;
- `writing.md` — maintained `SKILL.md` and `references/*.md` writing standard;
- `templates/agents.md` — maintained first-party Skill-repository `AGENTS.md` specialization.

## Progressive disclosure

Ordinary path:

```text
applicable AGENTS.md
→ this SKILL.md
→ one owning reference family
→ only the specific contract/template needed
```

Project design/redesign/conformance work additionally follows the target project's declared design-authority path before changing operational projections or implementation.

## Completion

Collaboration work is complete when the requested design/action/evidence reaches its declared terminal state and the applicable review/acceptance gate in `references/collaboration/protocol.md` is satisfied.
