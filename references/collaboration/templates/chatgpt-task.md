# ChatGPT formal task template

Use this template only for the **formal delegated task** path defined in `../protocol.md`.

Routine local execution does not require a committed task/report ceremony.

Formal Codex tasks live at:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

A formal task is issued only when ChatGPT can name the concrete local or otherwise unavailable capability that requires Codex and the work meets the formal-task gate in `../protocol.md`.

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

Use `../protocol.md` for collaboration/Git/concurrency rules and `../verification.md` for the selected verification level. Required changes and acceptance criteria should be directly checkable.

Commit and push the formal task before handoff; the committed task source is Codex's execution specification.

## Launch block

After the formal task is committed and pushed, give the User only this launch block rather than repeating the full specification:

```text
执行正式任务：

Repository:
<LOCAL_REPOSITORY>

Task:
reports/chatgpt/<TASK_FILE>.md

Task commit:
<TASK_COMMIT>

先 fetch 并确认当前仓库状态和 baseline。
严格执行 committed task，不依据聊天补充或扩大 scope。
完成实现、规定验证、Codex report、commit 和 push。
最后输出 task 要求的固定 stdout。
```
