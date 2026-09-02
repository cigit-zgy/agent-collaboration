# ChatGPT formal task template

Formal Codex tasks live at:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

A task is issued only when ChatGPT can name the concrete local or otherwise unavailable capability that requires Codex.

## Metadata

```yaml
---
artifact_type: chatgpt_task
task_id: <TASK_ID>
title: <SHORT_TITLE>
status: issued
date: <YYYY-MM-DD>
repository: <OWNER/REPOSITORY>
branch: <BRANCH>
baseline_sha: <BASELINE_SHA>
verification_level: <level_1 | level_2 | level_3>
summary: >
  <PURPOSE/SCOPE>
tags: []
concepts: []
codex_report: reports/codex/<YYMMDD_codex_NN.md>
---
```

## Body

```markdown
# <Task title>

## Mission
## Why Codex is required
## Current evidence / diagnosed problem
## Authoritative sources
## Scope
## Required changes
## Non-goals
## Scientific / product boundaries
## Engineering constraints
## Verification
## Acceptance criteria
## Git requirements
## Codex report
## Final stdout
```

Use `../protocol.md` for collaboration/Git rules and `../verification.md` for the selected verification level. Required changes and acceptance criteria should be directly checkable. Commit and push the task before handoff; the committed task source is Codex's execution specification.
