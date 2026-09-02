---
id: 03
title: Project integration and entry decisions
status: active
created: 2026-09-02
updated: 2026-09-02
role: decision_history
operational_authority:
  - references/project-integration.md
  - references/project-architecture.md
  - references/project-agents-template.md
  - references/project-skill-template.md
related_tasks: []
---

# Project integration and entry decisions

## Decision record

### 2026-09-02 — Project `AGENTS.md` is the constitution

- Decision: each maintained project uses root `AGENTS.md` for project-local
  authority, ownership, trust, runtime, and workflow routing.
- Rationale: project governance should remain local while global collaboration stays
  reusable.
- Operational authority: `references/project-integration.md`,
  `references/project-agents-template.md`.

### 2026-09-02 — Project workflow Skill path is declared, not fixed

- Decision: an Agent-operable project declares its workflow Skill path, commonly
  `<agent-name>/SKILL.md`; it is not required to be `project/SKILL.md`.
- Supersedes: the earlier fixed-root-path assumption.
- Rationale: multi-Skill research projects need a maintained Agent package without
  conflating project root governance and capability source.
- Operational authority: `references/project-integration.md`,
  `references/project-skill-template.md`.

### 2026-09-02 — Runtime reading path stays short

- Decision: ordinary project operation follows `AGENTS.md → workflow SKILL.md →
  owning sub-Skill → required resource`. Concepts are read only for historical design
  rationale/supersession.
- Supersedes: the earlier default route through concept index/topics before the
  project workflow Skill.
- Rationale: preserve progressive disclosure rather than creating a document
  traversal chain.
- Operational authority: `references/project-integration.md`.

### 2026-09-02 — Project initialization belongs to project architecture

- Decision: do not create a separate `project-initialization.md`; bootstrap rules and
  conditional directory triggers live in `project-architecture.md`.
- Rationale: keep ownership and creation criteria in one operational authority.
- Operational authority: `references/project-architecture.md`.
