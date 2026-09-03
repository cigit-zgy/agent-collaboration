# ChatGPT formal task template

Use only for the FORMAL route in `../protocol.md`. LOCAL-QUICK does not require a committed task/report.

Formal tasks live at:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

## Before issuing

ChatGPT must have:

```text
inspected current authority/evidence
→ partitioned DIRECT | LOCAL
→ completed task-specific DIRECT work
→ identified frozen semantic contracts/invariants
→ selected a dedicated task branch unless explicitly excepted
→ pinned the collaboration commit
→ selected verification level + concrete required evidence
```

Keep one formal task to one reviewable logical responsibility; split independent concerns.

## Metadata

```yaml
---
artifact_type: chatgpt_task
task_id: <TASK_ID>
title: <SHORT_TITLE>
status: issued
date: <YYYY-MM-DD>
repository: <OWNER/REPOSITORY>
task_branch: <TASK_BRANCH>
baseline_sha: <DIRECT_TASK_BASELINE_SHA>
verification_level: <level_1 | level_2 | level_3>
collaboration_commit: <PINNED_AGENT_COLLABORATION_SHA>
summary: >
  <PURPOSE/SCOPE>
codex_report: reports/codex/<YYMMDD_codex_NN.md>
---
```

`baseline_sha` is the task-branch commit after task-specific DIRECT inputs and before the task artifact. Supply the commit containing the task separately in the launch block as the execution handoff.

## Body

```markdown
# <Task title>

## Mission

## Authority and frozen semantics

Project authority:
- <governing project files>

Collaboration authority:
- cigit-zgy/agent-collaboration@<SHA>:SKILL.md
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/protocol.md
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/implementation.md
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/verification.md
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/templates/codex-report.md

<Frozen scientific/product/design contracts Codex must not reinterpret.>

## LOCAL scope

<What Codex owns and why local/runtime capability is required.>

## Required changes

## Non-goals / ownership boundary

## Engineering constraints

<Only task-specific constraints. General AI implementation policy comes from implementation.md; mechanical style comes from project tooling.>

## Acceptance criteria

## Verification

Verification level: LEVEL 1 | LEVEL 2 | LEVEL 3

Required evidence:
- <category>: <concrete check>
- ...

## Git handoff / integration

<Task branch, same-branch exception if any, integration condition.>

## Codex report

reports/codex/<YYMMDD_codex_NN.md>
```

List only verification categories actually required; no mandatory `N/A` matrix.

For an upstream owner where downstream migration is out of scope, the task should state that stale consumers are reported rather than repaired and rejected upstream interfaces are not restored for compatibility.

A narrowly mechanical projection edit is permitted only when the task names that permission and it cannot alter frozen semantics. A design conflict stops the affected implementation for User + ChatGPT adjudication.

## User-visible handoff link — hard requirement

After the formal task is committed and pushed, ChatGPT MUST prominently surface a directly openable link to the exact committed task before or immediately adjacent to the Codex launch text:

```text
任务链接如下：
https://github.com/<OWNER>/<REPOSITORY>/blob/<TASK_COMMIT>/reports/chatgpt/<TASK_FILE>.md
```

`<TASK_COMMIT>` is the execution handoff commit that contains the task. Use the full HTTPS GitHub URL, not only the repository-relative path or commit SHA. This link is part of the required User-facing handoff contract so the User can inspect the exact task without reconstructing a repository URL manually.

If the task was not successfully pushed, do not fabricate the link. Show `任务链接如下：UNAVAILABLE` with the publication blocker and do not represent the formal handoff as complete.

## Launch block

After committing/pushing the task, give the User the prominent task link above followed by this launch block:

```text
执行正式任务：

Repository:
<LOCAL_REPOSITORY>

Task:
reports/chatgpt/<TASK_FILE>.md

Task branch:
<TASK_BRANCH>

Task commit / execution handoff:
<TASK_COMMIT>

Collaboration authority:
cigit-zgy/agent-collaboration@<PINNED_AGENT_COLLABORATION_SHA>

先 fetch，并检查 branch / HEAD / upstream / worktree。
安全到达 exact task branch + handoff commit 后开始实现。
严格执行 committed task，不依据聊天扩大 scope。
使用 pinned collaboration authority；不以未验证本地副本替代。
不得 reinterpret task 冻结的 design semantics；发现设计冲突时停止相关实现并报告。
代码遵循 implementation.md：最小充分、可审查、透明，AI 代码与人工代码同一质量标准。
按 verification level + required evidence 完成验证。
完成 Codex report、task-scoped commit 和 task-branch push。
最终控制台必须按 codex-report.md 显眼输出可直接打开的 immutable GitHub 报告链接，不能只给本地路径或仓库相对路径。
ChatGPT acceptance review 后再集成 default branch。
```
