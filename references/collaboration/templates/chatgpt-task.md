# ChatGPT FORMAL task template

Load only when creating or reviewing a FORMAL task.

FORMAL lifecycle is owned by `../formal.md`; execution safety, tmp/worktree placement, branch hygiene, and concurrency by `../execution.md`; verification by `../verification.md`.

Tasks live at `reports/chatgpt/YYMMDD_chatgpt_NN.md`. The committed task is the sole task-specific execution specification; chat contains only the locator.

## Metadata

```yaml
---
artifact_type: chatgpt_record
artifact_id: <YYMMDD_chatgpt_NN>
record_kind: task
task_id: <TASK_ID>
title: <SHORT_TITLE>
date: <YYYY-MM-DD>
project: <PROJECT_NAME>
repository: <OWNER/REPOSITORY>
status: issued
execution_mode: formal
summary: >
  <ONE-SENTENCE OUTCOME>
task_branch: <TASK_BRANCH>
baseline_sha: <AUTHORIZED_BASELINE_SHA>
verification_level: <level_1 | level_2 | level_3>
collaboration_commit: <PINNED_AGENT_COLLABORATION_SHA>
codex_report: reports/codex/<YYMMDD_codex_NN.md>
mutation_scope:
  - <REPOSITORY_RELATIVE_PATH_OR_SEMANTIC_OWNER>
concurrency_keys: []
design_topics: []
design_signal: none
---
```

For repository-changing work, `mutation_scope` is required. Use compact path/owner boundaries rather than an exhaustive file inventory. Add `concurrency_keys` for shared semantic owners/resources; use the same key across tasks that must serialize. Shared authority surfaces such as `AGENTS.md`, `CURRENT.md`, `reports/design/**`, shared Skill semantics, or central schema/public-interface owners serialize by default under the current execution contract.

One task uses at most one task branch. Ordinary repair remains on that branch; do not create extra repair/experiment branches.

Add other coordinates only when they materially govern the task.

## Preferred body

```markdown
# <Task title>

## Mission
<Final state to achieve.>

## Authority and boundaries
<Owners and semantics that must not be reinterpreted.>

## Scope
<What may change and material non-goals.>

## Completion criteria
<Observable conditions that mean the task is done.>

## Required evidence
<Only checks needed to establish completion.>

## User decision points
<Only choices that truly require User/ChatGPT input.>

## Result contract
<Compact terminal fields and report path.>
```

Prefer outcome-oriented instructions. Do not prescribe a command-by-command path unless the sequence itself is required for correctness or reproducibility.

Within scope, Codex may inspect, implement, run, diagnose, repair, and rerun until completion criteria are met.

Repository-changing Codex work normally uses one linked worktree at `<PROJECT_ROOT>/tmp/<WORK_ID>/worktree/`. That worktree is a real Git checkout; durable source/docs/design/report changes are edited at their normal repository-relative paths and must be committed/published before completion.

## User-visible locator

After commit/push, emit only the short locator:

```text
执行 FORMAL 任务：
Repository: <LOCAL_REPOSITORY_OR_OWNER/REPO>
Task: reports/chatgpt/<TASK_FILE>.md
Task commit: <TASK_COMMIT>
任务链接如下：
https://github.com/<OWNER>/<REPOSITORY>/blob/<TASK_COMMIT>/reports/chatgpt/<TASK_FILE>.md
以 committed task 为唯一 task-specific 执行规范。
```

Do not repeat the task body in chat.
