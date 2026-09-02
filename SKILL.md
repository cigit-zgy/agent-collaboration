---
name: agent-collaboration
description: >
  Coordinate User, ChatGPT, and Codex for repository work involving design, direct remote action,
  local implementation, verification, acceptance, project integration, or Skill maintenance.
---

# Agent Collaboration

## Purpose

This Skill routes the collaboration contract for:

```text
User ↔ ChatGPT ↔ Codex
```

Load only the reference family that owns the active concern.

## Core route

For design, delegation, local execution, verification, and acceptance, read:

```text
references/collaboration/protocol.md
```

The stable role split is:

```text
User + ChatGPT = design and acceptance
ChatGPT        = direct executor when connected capabilities are sufficient
Codex          = local executor when genuinely local/unavailable capability is required
```

Evidence determines acceptance; Codex does not self-accept.

## Reference routing

### Collaboration

Use `references/collaboration/` for the three-party operating loop:

- `protocol.md` — roles, delegation, Git synchronization, acceptance;
- `verification.md` — verification levels and risk-based tool selection;
- `agents.md` — collaboration-wide `AGENTS.md` writing standard;
- `templates/` — formal ChatGPT task, Codex launch, and Codex report formats.

### Project

Use `references/project/` when a scientific/software project joins this collaboration:

- `architecture.md` — project entry, repository ownership, authority hierarchy, reading modes, onboarding;
- `concept.md` — `reports/concept/` design-authority contract;
- `templates/agents.md` — project root `AGENTS.md`;
- `templates/skill.md` — project workflow `SKILL.md`.

### Skill

Use `references/skill/` for first-party/third-party Skill ownership and package design:

- `repository.md` — maintained source, discovery, distribution, rename lifecycle;
- `package.md` — package resources, profiles, runtime/environment ownership;
- `writing.md` — maintained `SKILL.md` writing standard;
- `templates/agents.md` — maintained first-party Skill-repository `AGENTS.md`.

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

Collaboration work is complete when the requested design/action/evidence has reached its declared terminal state and the relevant acceptance gate in `references/collaboration/protocol.md` has been satisfied.
