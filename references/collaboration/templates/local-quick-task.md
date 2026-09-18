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
mutation_scope: []
concurrency_keys: []
design_topics: []
design_signal: none
---
```

For repository-changing work, also include the authorized branch/baseline coordinates needed to recover the task state and fill `mutation_scope` with compact repository-relative paths or semantic owners. Add `concurrency_keys` when the task shares a mutable semantic owner/resource with other tasks.

One repository-changing task uses at most one task branch. Ordinary repair remains on that branch; do not create extra repair/experiment branches.

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

For repository-changing Codex work, use the execution contract's default linked worktree at `<PROJECT_ROOT>/tmp/<WORK_ID>/worktree/` when isolation is needed or concurrent work exists. The worktree is a real Git checkout: retained project files are edited at their normal repository-relative locations and must be committed/published; accepted output must not exist only as an uncommitted tmp file.

If work expands into a material scientific/product decision, destructive/shared-state change, public/release action, or another FORMAL boundary, stop the affected path and report the concrete escalation reason.

## Codex record

Codex writes the bound concise `reports/codex/` record using `codex-report.md` with `record_kind: local_quick`.

The record preserves:

```text
what changed
focused evidence
final repository coordinate
worktree/branch disposition when repository-changing
limitations/blocker
design_signal
```

Do not inflate it into a FORMAL narrative.

## User-visible task link

After commit/push, emit exactly one copyable fenced block:

```text
任务链接：
https://github.com/<OWNER>/<REPOSITORY>/blob/<TASK_COMMIT>/reports/chatgpt/<TASK_FILE>.md
```

Do not add repository/task coordinates, task steps, explanations, or prose after the block unless the User explicitly asks.
