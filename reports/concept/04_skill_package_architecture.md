---
id: 04
title: Skill source, discovery, and package decisions
status: active
created: 2026-09-02
updated: 2026-09-02
role: decision_history
operational_authority:
  - references/skill-repository-policy.md
  - references/skill-package-architecture.md
  - references/skill-agents-template.md
  - references/skill-templates/README.md
related_tasks: []
---

# Skill source, discovery, and package decisions

## Decision record

### 2026-09-02 — Minimal Skill package with purpose profiles

- Decision: `SKILL.md` is the required capability entry; references/scripts/assets/
  tests/runtime/README are conditional. Documentation, executable, asset-oriented,
  and composite/router profiles use different minimal scaffolds.
- Rationale: avoid empty directories, speculative abstractions, and unnecessary
  runtimes while preserving progressive disclosure.
- Operational authority: `references/skill-package-architecture.md`,
  `references/skill-templates/README.md`.

### 2026-09-02 — Maintained source repository differs from runtime package

- Decision: a standalone first-party maintained source repository retains root
  `AGENTS.md` for maintenance, while a portable Skill runtime/distribution may omit
  maintenance-only assets.
- Rationale: repository maintenance and Skill consumption are separate lifecycle
  concerns.
- Operational authority: `references/skill-agents-template.md`,
  `references/skill-package-architecture.md`.

### 2026-09-02 — Discovery exposure differs from maintained source

- Decision: `/Users/wenv/Documents/skills/<name>/` remains first-party maintained
  source, while Codex discovery uses current `.agents/skills` locations. User-scoped
  discovery normally uses a symlink from `$HOME/.agents/skills/<name>` to maintained
  source; reusable external distribution should prefer supported plugins.
- Supersedes: the earlier assumption that maintained source itself was sufficient for
  Codex discovery and that first-party discovery symlinks should be prohibited.
- Rationale: align local source ownership with current OpenAI Codex discovery without
  creating duplicate maintained copies.
- Operational authority: `references/skill-repository-policy.md`.
