---
id: 02
title: Three-party collaboration decisions
status: active
created: 2026-09-02
updated: 2026-09-02
role: decision_history
operational_authority:
  - references/protocol.md
  - references/chatgpt-task-template.md
  - references/codex-launch-template.md
  - references/codex-report-template.md
related_tasks: []
---

# Three-party collaboration decisions

## Decision record

### 2026-09-02 — User + ChatGPT design, Codex executes

- Decision: User + ChatGPT own architecture, scientific/product semantics, scope,
  constraints, and acceptance decisions. Codex executes committed local tasks and
  does not silently redesign them.
- Rationale: separate design authority from local execution and make acceptance
  independent of executor self-report.
- Operational authority: `references/protocol.md`.

### 2026-09-02 — Delegate only for a concrete unavailable/local capability

- Decision: ChatGPT performs repository work directly when connected tools are
  sufficient. A formal Codex task requires an explicit `Why Codex is required`
  capability gap.
- Rationale: avoid unnecessary handoff latency and design ambiguity.
- Operational authority: `references/protocol.md`,
  `references/chatgpt-task-template.md`.

### 2026-09-02 — One formal task at a time, evidence-based acceptance

- Decision: Codex executes one committed task, returns execution evidence, and
  ChatGPT independently audits before another formal task begins.
- Rationale: preserve a single auditable task boundary and prevent self-acceptance.
- Operational authority: `references/protocol.md`,
  `references/codex-report-template.md`.
