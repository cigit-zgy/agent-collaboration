# ChatGPT FORMAL task template

Cold path: load this file only when creating or reviewing a FORMAL task artifact.

FORMAL lifecycle/acceptance/integration is owned by `../formal.md`; report filename/common metadata/archive rules by `../../project/reports.md`; local Git/worktree/tmp mechanics by `../execution.md`; verification evidence design by `../verification.md`.

Formal tasks live only at:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

## Before issuing

ChatGPT must have:

```text
refreshed current collaboration authority for this repository-changing work unit
→ inspected current project authority/evidence
→ completed design-bearing decisions before task issue
→ for Skill behavior changes: updated governing concept/design + SKILL.md/references first
→ partitioned ChatGPT-authorable work from genuinely local work
→ completed DIRECT code/tests/checks it can correctly perform
→ resolved activated shared coding-Skill authorities
→ selected verification level + remaining evidence
→ selected dedicated task branch unless explicitly excepted
→ pinned the exact collaboration revision
```

Keep one FORMAL task to one reviewable logical responsibility.

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

`artifact_id` equals the filename stem. `baseline_sha` is the task-branch commit after task-specific ChatGPT DIRECT inputs and before the task artifact. `codex_report` is the exact expected report path; changing it requires a durable amendment/superseding task.

## Body

Use the smallest task body that fully specifies execution. Typical sections are:

```markdown
# <Task title>

## Mission
## Authority and frozen semantics
## Shared coding Skills and authoring state
## LOCAL scope
## Required changes
## Non-goals / ownership boundary
## Engineering constraints
## Acceptance criteria
## Verification
## Git handoff / integration
## Codex report
```

Bind exact governing concept/design + committed `SKILL.md`/reference owners for Skill behavior changes. List only verification categories actually required; no mandatory `N/A` matrix.

## Skill behavior tasks — hard requirement

A FORMAL task is an execution specification, not a substitute for the Skill contract.

```text
User + ChatGPT concept/design adjudication
→ governing concept/design updated
→ SKILL.md + references updated
→ committed task points to those exact Markdown owners
→ Codex implements/repairs code to conform
→ tests probe the general Skill contract
```

Codex MUST NOT create a task-specific production patch merely to satisfy one triggering example when durable Skill semantics are missing/ambiguous. If local execution discovers a new design gap, classify/report `DESIGN_GAP` and stop the affected implementation path. Pure implementation drift may proceed when the durable contract already determines expected behavior without interpretation.

## ChatGPT-first authoring

ChatGPT completes code/tests it can correctly author before handoff. Local verification need alone does not transfer all implementation authorship to Codex.

## User-visible handoff

After commit/push, provide a concise informational synopsis plus one copyable Markdown fenced `text` block. The synopsis must not add task semantics absent from the committed file.

Exact launch block shape:

```text
执行正式任务：

Repository: <LOCAL_REPOSITORY>
Task: reports/chatgpt/<TASK_FILE>.md
Task branch: <TASK_BRANCH>
Task commit: <TASK_COMMIT>
Collaboration: cigit-zgy/agent-collaboration@<PINNED_AGENT_COLLABORATION_SHA>

任务链接如下：
https://github.com/<OWNER>/<REPOSITORY>/blob/<TASK_COMMIT>/reports/chatgpt/<TASK_FILE>.md

以 committed task 为唯一 task-specific 执行规范；使用 pinned collaboration、shared coding-Skill profile 和 project authority 执行实现与验证。
```

If the task was not successfully pushed, do not fabricate a remote link. Do not append task-specific implementation detail after the copyable block.
