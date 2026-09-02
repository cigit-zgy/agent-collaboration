---
id: 01
title: Report Asset Metadata Policy
status: active
created: 2026-09-02
updated: 2026-09-02
authority: global
scope: structured metadata and retrieval rules for ChatGPT tasks and Codex reports
supersedes: null
related_tasks: []
---

# Report Asset Metadata Policy

## 2026-09-02

### Decision

New `reports/chatgpt/*.md` and `reports/codex/*.md` artifacts must begin with compact YAML front matter so tasks and implementation reports can be searched, filtered, paired, and summarized without reading the full body.

ChatGPT task metadata records task identity, repository scope, baseline, verification level, a concise summary, stable tags, governing concept assets, and the expected Codex report path.

Codex report metadata records the paired task identity and task-source SHA, verdict, repository scope, baseline, verification level, a concise implementation/result summary, stable tags, governing concepts, and material non-blocking limitations.

Self-referential commit metadata is prohibited: a ChatGPT task does not contain the commit SHA that contains that task, and a Codex report does not contain the commit SHA that contains that report. Those values remain available from Git history and fixed stdout.

### Rationale

Task and report counts will grow over time. Structured front matter provides a stable retrieval surface while keeping the human-readable report body free to explain evidence and decisions. Compact metadata also avoids inventing separate indexes, manifests, or databases solely for report discovery.

### Impact

- `references/chatgpt-task-template.md`
- `references/codex-report-template.md`
- `references/report-concept-policy.md`
- future project `reports/chatgpt/` and `reports/codex/` artifacts

Historical reports do not require retrospective migration unless a specific task needs it.

### Related tasks

None. This policy was established directly as a durable collaboration asset.
