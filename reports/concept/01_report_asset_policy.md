---
id: 01
title: Report asset lifecycle decisions
status: active
created: 2026-09-02
updated: 2026-09-02
role: decision_history
operational_authority:
  - references/report-concept-policy.md
  - references/chatgpt-task-template.md
  - references/codex-report-template.md
related_tasks: []
---

# Report asset lifecycle decisions

## Decision record

### 2026-09-02 — Structured task/report metadata

- Decision: formal ChatGPT tasks and Codex reports use compact YAML front matter for
  identity, retrieval, and task/report linkage.
- Rationale: make artifacts searchable and machine-readable without speculative
  metadata.
- Operational authority: `references/report-concept-policy.md` and the two report
  templates.

### 2026-09-02 — Keep issued task/report paths stable

- Decision: remove calendar-based weekly archives. Once a formal task or Codex report
  is issued/committed, its repository-relative path remains stable and the artifact is
  not rewritten merely to represent later lifecycle state.
- Supersedes: the earlier weekly `git mv` archive scheme and post-execution mutation
  of task metadata/links.
- Rationale: `task_source_sha` must continue to refer to the exact committed task
  Codex executed; stable artifacts reduce provenance complexity.
- Operational authority: `references/report-concept-policy.md`.

### 2026-09-02 — Remove duplicate body metadata

- Decision: identity fields live once in YAML; task/report bodies contain mission,
  evidence, verification, and results rather than a second copy of IDs, dates,
  repository, branch, baseline, or status.
- Rationale: avoid two editable representations of the same metadata.
- Operational authority: `references/chatgpt-task-template.md`,
  `references/codex-report-template.md`.
