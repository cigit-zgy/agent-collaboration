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
  - 260902_chatgpt_02
  - 260902_chatgpt_03
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

### Additional decision — synchronization, verification, environments, and speed

Formal Codex repository work must begin from an explicit fetched Git state and end
with the local task branch synchronized to its configured upstream. Codex preserves
pre-existing user changes, performs only safe fast-forward synchronization, commits
and pushes task-scoped changes, fetches again, and normally verifies
`HEAD == upstream`. Divergence or unsafe dirty state must be reported rather than
resolved through an invented merge/rebase, destructive reset, force-push, or
unapproved stash.

Ordinary development defaults to `LEVEL 1 — FOCUSED`. Verification is intentionally
fast and risk-proportional: affected tests and the smallest useful smoke/integration
check are preferred over full-suite testing, clean-environment rebuilds, repeated
reviewers, or release-grade scanning.

For adversarial/static verification, Semgrep Community Edition is the preferred
fast targeted scanner for security-sensitive changed surfaces. CodeQL is the deeper
semantic/data-flow tool used primarily for release/security gates when supported;
`pip-audit` complements these for Python dependency vulnerability checks. These
tools are selected by risk and verification level, not run on every task.

Environment ownership follows executable code rather than Skill count. Documentation-
only Skills have no environment. Project-executed code uses the project's declared
environment. An independently executable first-party Skill may own a runtime only
when it has a real consumer. Healthy environments are reused; clean rebuilds are
reserved for reproducibility, release, or demonstrably invalid environments.

### Rationale

The collaboration protocol must keep GitHub and local state auditable without
turning synchronization into destructive ceremony. Security tools and clean
environments are useful only when they cover a defined risk. Fast focused feedback
is the default development mode; broader evidence belongs to major or release work.

### Impact

- `references/protocol.md`
- `references/chatgpt-task-template.md`
- `references/codex-report-template.md`
- `references/verification-levels.md`
- `references/verification-tools.md`
- `references/skill-environment-policy.md`
- the concise machine-wide routing rules in `~/.codex/AGENTS.md`

### Related tasks

- 260902_chatgpt_02

### Additional decision — machine-wide verification utility installation

Semgrep, CodeQL CLI, and `pip-audit` are adopted as machine-wide third-party developer utilities. On this macOS workstation they are installed outside project runtimes, preferably through Homebrew, so verification capability does not mutate project Conda/venv dependencies. Installation alone does not trigger their use: Level 1 remains scanner-free by default, and each tool is invoked only when the selected verification level and risk justify it. CodeQL execution must respect current GitHub licensing and repository eligibility.

### Rationale

Keeping these utilities machine-wide makes them available when a security/release task needs them while preserving project environment boundaries and fast ordinary development.

### Impact

- `references/verification-tools.md`
- `references/skill-environment-policy.md`
- machine-level Homebrew installation state

### Related tasks

- 260902_chatgpt_03
