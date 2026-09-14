# ChatGPT LOCAL-QUICK task template

Load only when creating or reviewing a LOCAL-QUICK task.

Every LOCAL-QUICK repository task is committed at `reports/chatgpt/YYMMDD_chatgpt_NN.md`. Chat contains only the locator.

## Metadata

```yaml
---
artifact_type: chatgpt_task
artifact_id: <YYMMDD_chatgpt_NN>
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
---
```

For repository-changing work, also include the authorized branch/baseline coordinates needed to recover the task state.

## Preferred body

```markdown
# <Task title>

## Mission
<Final state to achieve.>

## Authority and boundaries
<Owners and constraints that must not be reinterpreted.>

## Scope
<What may change and material non-goals.>

## Completion criteria
<Observable conditions that mean the task is done.>

## Required evidence
<Only checks needed to establish completion.>

## User decision points
<Usually NONE for LOCAL-QUICK.>

## Result contract
<Compact terminal fields.>
```

Do not turn LOCAL-QUICK into a command recipe. Inside the authorized scope, Codex may inspect, implement, verify, diagnose, repair, and rerun until completion criteria are met.

If work expands into a material scientific/product decision, destructive/shared-state change, public/release action, or another FORMAL boundary, stop that affected path and return the concrete escalation reason.

LOCAL-QUICK does not create `reports/codex/`.

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
