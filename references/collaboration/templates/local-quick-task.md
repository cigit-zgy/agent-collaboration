# ChatGPT LOCAL-QUICK task template

Load only when creating or reviewing a LOCAL-QUICK task.

Every LOCAL-QUICK repository task uses:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
reports/codex/YYMMDD_codex_NN.md
```

Chat contains only the task locator. The Codex record is concise and append-only.

## Metadata

```yaml
---
artifact_type: chatgpt_record
artifact_id: <YYMMDD_chatgpt_NN>
record_kind: task
task_id: <SHORT_TASK_ID>
title: <SHORT_TITLE>
date: <YYYY-MM-DD>
project: <PROJECT_NAME>
repository: <OWNER/REPOSITORY>
status: issued
execution_mode: local_quick
summary: >
  <ONE-SENTENCE OUTCOME>
collaboration_commit: <PINNED_AGENT_COLLABORATION_SHA>
codex_report: reports/codex/<YYMMDD_codex_NN.md>
design_topics: []
design_signal: none
---
```

For repository-changing work, also include the authorized branch/baseline coordinates needed to recover the task state.

## Preferred body

```markdown
# <Task title>

## Mission
## Authority and boundaries
## Scope
## Completion criteria
## Required evidence
## User decision points
## Result contract
```

Use only the sections the task actually needs. Do not turn LOCAL-QUICK into a command recipe.

Inside authorized scope, Codex may inspect, implement, verify, diagnose, repair, and rerun until completion criteria are met.

If work expands into a material scientific/product decision, destructive/shared-state change, public/release action, or another FORMAL boundary, stop the affected path and report the concrete escalation reason.

## Codex record

Codex writes the bound concise `reports/codex/` record using `codex-report.md` with `record_kind: local_quick`.

The record preserves:

```text
what changed
focused evidence
final repository coordinate
limitations/blocker
design_signal
```

Do not inflate it into a FORMAL narrative.

## User-visible locator

```text
执行 LOCAL-QUICK 任务：
Repository: <LOCAL_REPOSITORY_OR_OWNER/REPO>
Task: reports/chatgpt/<TASK_FILE>.md
Task commit: <TASK_COMMIT>
任务链接如下：
https://github.com/<OWNER>/<REPOSITORY>/blob/<TASK_COMMIT>/reports/chatgpt/<TASK_FILE>.md
以 committed task 为唯一 task-specific 执行规范；完成后只按 task 的 Result contract 返回结果。
```

Do not repeat the task body in chat.
