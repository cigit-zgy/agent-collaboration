# ChatGPT FORMAL task template

Cold path: load only when creating/reviewing a FORMAL task.

FORMAL lifecycle is owned by `../formal.md`; report layout by `../../project/reports.md`; Git/tmp by `../execution.md`; verification by `../verification.md`.

FORMAL tasks live at:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

The committed task is the sole task-specific execution specification. Detailed task content must not be repeated in chat.

## Before issuing

ChatGPT must have:

```text
refreshed current collaboration authority
→ inspected current project authority/evidence
→ completed design-bearing decisions
→ for Skill behavior changes: updated reports/design/ + SKILL.md/references first
→ completed ChatGPT-authorable DIRECT work
→ resolved shared coding-Skill authority
→ selected verification level
→ selected task branch unless explicitly excepted
→ pinned exact collaboration revision
```

## Required metadata

```yaml
---
artifact_type: chatgpt_task
artifact_id: <YYMMDD_chatgpt_NN>
task_id: <TASK_ID>
title: <SHORT_TITLE>
date: <YYYY-MM-DD>
project: <PROJECT_NAME>
repository: <OWNER/REPOSITORY>
status: issued
execution_mode: formal
summary: >
  <PURPOSE/SCOPE>
task_branch: <TASK_BRANCH>
baseline_sha: <DIRECT_TASK_BASELINE_SHA>
verification_level: <level_1 | level_2 | level_3>
collaboration_commit: <PINNED_AGENT_COLLABORATION_SHA>
coding_skill_profile: >
  cigit-zgy/agent-collaboration@<PINNED_AGENT_COLLABORATION_SHA>:
  references/collaboration/shared-coding-skills.md
codex_report: reports/codex/<YYMMDD_codex_NN.md>
---
```

## Body

Use the smallest body that fully specifies execution. Bind exact `reports/design/` topic(s) plus committed Skill/reference owners for design-bearing Skill changes.

## Remote synchronization — hard requirement

Before mutation:

```text
fresh-fetch
→ resolve exact task branch/task/baseline
→ inspect local branch/HEAD/upstream/worktrees/User state
→ establish safe task worktree
→ prove local execution HEAD == authorized fetched baseline
```

After changes:

```text
commit task-scoped changes
→ push task branch
→ fresh-fetch again
→ prove local task HEAD == fetched upstream HEAD
→ record evidence in Codex report
```

Without final equality, PASS is forbidden. Do not use blind pull/reset/rebase/stash/force operations merely to synchronize.

## Skill behavior tasks

```text
User + ChatGPT adjudication
→ reports/design/ updated
→ SKILL.md + references updated
→ committed task points to those exact owners
→ Codex implements/repairs code
→ tests probe the general contract
```

A new `DESIGN_GAP` stops the affected implementation path.

## User-visible locator

After commit/push, at most one short sentence may precede exactly one fenced `text` block:

```text
执行 FORMAL 任务：
Repository: <LOCAL_REPOSITORY_OR_OWNER/REPO>
Task: reports/chatgpt/<TASK_FILE>.md
Task commit: <TASK_COMMIT>
任务链接如下：
https://github.com/<OWNER>/<REPOSITORY>/blob/<TASK_COMMIT>/reports/chatgpt/<TASK_FILE>.md
以 committed task 为唯一 task-specific 执行规范。
```

Do not repeat task steps or append task-specific prose after the locator.
