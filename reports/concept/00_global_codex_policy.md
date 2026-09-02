---
id: 00
title: Global Codex operating-policy decisions
status: active
created: 2026-09-02
updated: 2026-09-02
role: decision_history
operational_authority:
  - references/protocol.md
  - references/skill-repository-policy.md
  - references/verification-levels.md
  - references/verification-tools.md
  - references/skill-environment-policy.md
related_tasks:
  - 260902_chatgpt_01
  - 260902_chatgpt_02
  - 260902_chatgpt_03
---

# Global Codex operating-policy decisions

## Decision record

### 2026-09-02 — Keep machine-wide instructions small and layered

- Decision: `~/.codex/AGENTS.md` is the machine-wide Codex instruction entry; project
  `AGENTS.md` files provide more specific repository guidance.
- Rationale: global instructions should remain concise and delegate detailed workflow
  to Skills/references.
- Operational authority: `references/protocol.md` plus the machine-local AGENTS file.
- Related tasks: `260902_chatgpt_01`.

### 2026-09-02 — Risk-proportional verification and environment ownership

- Decision: ordinary work uses focused verification; Semgrep/CodeQL/pip-audit are
  selected by risk, and environments follow executable ownership rather than Skill
  count.
- Rationale: preserve scientific/product rigor without making every change
  release-grade.
- Operational authority: `references/verification-levels.md`,
  `references/verification-tools.md`, `references/skill-environment-policy.md`.
- Related tasks: `260902_chatgpt_02`, `260902_chatgpt_03`.

### 2026-09-02 — Correct Codex Skill discovery model

- Decision: `/Users/wenv/Documents/skills/` remains the maintained first-party source
  root, but current Codex discovery is exposed through `.agents/skills` locations.
  User-scoped first-party discovery normally uses
  `$HOME/.agents/skills/<name> → symlink → maintained source`. Reusable external
  distribution should prefer supported plugins.
- Supersedes: the earlier assumption that `~/.codex/skills/` was the canonical
  current discovery location and that first-party discovery symlinks should be
  prohibited.
- Rationale: align maintained source ownership with current OpenAI Codex discovery
  while retaining a single first-party source copy.
- Operational authority: `references/skill-repository-policy.md`.
- Related tasks: none yet; local reconciliation requires a follow-up Codex task.
