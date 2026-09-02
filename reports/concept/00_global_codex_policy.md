---
id: 00
title: Global Codex Operating Policy
status: active
created: 2026-09-02
updated: 2026-09-02
authority: global
scope: machine-wide Codex defaults, Skill ownership/routing, collaboration, and verification discipline
supersedes: null
related_tasks:
  - 260902_chatgpt_01
---

# Global Codex Operating Policy

## 2026-09-02

### Decision

`~/.codex/AGENTS.md` is the machine-wide Codex operating entry point. It supplies global defaults only; explicit User instructions and more specific project `AGENTS.md` files remain more specific authorities.

Skills use only two ownership classes:

- `FIRST_PARTY`: designed and maintained by the User; source lives under `/Users/wenv/Documents/skills/` and is tracked in `LOCAL_SKILLS.md`.
- `THIRD_PARTY`: maintained upstream; consumed through `~/.codex/skills/`, `~/.codex/upstream/`, or an official Codex plugin without duplicate discovery.

The global AGENTS file routes repository collaboration to `/Users/wenv/Documents/skills/agent-collaboration/SKILL.md`; it does not duplicate that Skill's templates or protocol.

Default routing is selective rather than load-all:

- Superpowers: non-trivial planning, debugging, implementation workflow, review, and verification.
- Ponytail `full`: smallest sufficient engineering for coding tasks; never removes an explicit scientific, product, security, or trust-boundary invariant.
- `scientific-python`: scientific/numerical Python work.
- `modern-python`: Python modernization/tooling when specifically relevant.
- `ask-human`: genuine human decisions or approvals.
- `task-progress`: long-running tasks that benefit from milestone progress.
- `repository-audit`: repository-wide readiness/audit work.
- `open-sourcing` and `release`: release/open-source stages only.

Verification follows the level selected by the formal task. Codex must not add hashes, manifests, freshness layers, abstractions, or duplicate tests merely for reassurance; each such mechanism needs a current consumer or protected trust boundary.

Two first-party renames are adopted:

- `axiomfig-skill` → `axiomfig`
- `sci-manuscript-skill` → `sci-manuscript`

Each rename must update the local folder, `SKILL.md` name, GitHub repository name, `origin`, `LOCAL_SKILLS.md`, and active non-historical routing references together.

### Rationale

The global file should be small enough to remain reliable in every Codex session while delegating detailed procedure to Skills. Two ownership classes are sufficient for the actual machine layout and avoid unnecessary distinctions between an upstream repository and a Skill extracted from one.

### Impact

- `~/.codex/AGENTS.md`
- `/Users/wenv/Documents/skills/LOCAL_SKILLS.md`
- `references/skill-repository-policy.md`
- the two renamed first-party Skill repositories
- future project-level `AGENTS.md` files, which may add project-specific rules without copying the global collaboration protocol

### Related tasks

- 260902_chatgpt_01
