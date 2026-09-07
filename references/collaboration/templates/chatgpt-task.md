# ChatGPT FORMAL task template

Cold path: load this file only when creating or reviewing a FORMAL task artifact.

FORMAL lifecycle/acceptance/integration is owned by `../formal.md`; local Git/worktree/tmp mechanics by `../execution.md`; verification evidence design by `../verification.md`.

Formal tasks live at:

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
coding_skill_profile: >
  cigit-zgy/agent-collaboration@<PINNED_AGENT_COLLABORATION_SHA>:
  references/collaboration/shared-coding-skills.md
summary: >
  <PURPOSE/SCOPE>
codex_report: reports/codex/<YYMMDD_codex_NN.md>
---
```

`baseline_sha` is the task-branch commit after task-specific ChatGPT DIRECT inputs and before the task artifact. The launch locator separately supplies the commit containing the task.

`codex_report` is the exact expected report path. Codex MUST publish there on `task_branch`; changing it requires a durable amendment/superseding task.

## Body

````markdown
# <Task title>

## Mission

## Authority and frozen semantics

Project authority:
- <governing project files>

Collaboration authority:
- cigit-zgy/agent-collaboration@<SHA>:SKILL.md
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/protocol.md
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/execution.md
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/formal.md
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/implementation.md
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/shared-coding-skills.md
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/verification.md
- <ACTIONS OWNER ONLY IF THIS TASK ACTUALLY USES/CHANGES GITHUB ACTIONS>
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/templates/codex-report.md

<Frozen scientific/product/design/Skill contracts Codex must not reinterpret.>

For Skill behavior changes, also bind exact governing concept/design + committed SKILL.md/reference owners.

## Shared coding Skills and authoring state

Shared profile:
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/shared-coding-skills.md

Activated shared Skills:
- <SKILL_NAME> — <MODE/ACTIVATION>

Additional project/task Skill authorities:
- <NONE OR OWNER/REPO@COMMIT:PATH — MODE>

ChatGPT-authored before handoff:
- <PATHS OR NONE + REASON>

ChatGPT checks already completed:
- <CHECK + RESULT OR NONE>

Remaining Codex-local work:
- <LOCAL VERIFICATION / BOUNDED REPAIR / LOCAL-FEEDBACK-DEPENDENT IMPLEMENTATION>

## LOCAL scope

<What Codex owns and why local/runtime capability is required.>

## Required changes

## Non-goals / ownership boundary

## Engineering constraints

<Only task-specific constraints; do not copy global collaboration manuals.>

## Acceptance criteria

## Verification

Verification level: LEVEL 1 | LEVEL 2 | LEVEL 3

ChatGPT checks already completed:
- <check>: <result>

Remaining Codex-local evidence:
- <category>: <concrete check>

Shared coding-Skill alignment:
- verify only activated Skills against the task-pinned profile

Temporary-state closure:
- clean task-local temporary state, or report exact retained recovery state + reason

## Git handoff / integration

Task branch: <TASK_BRANCH>
Target integration branch: <TARGET_BRANCH>
Post-acceptance integration: AUTO | USER_CHECKPOINT
Local temporary workspace: <PROJECT_ROOT>/tmp/<TASK_ID>/
<Any explicitly User-authorized exception.>

## Codex report

reports/codex/<YYMMDD_codex_NN.md>
````

List only verification categories actually required; no mandatory `N/A` matrix.

## Skill behavior tasks — hard requirement

A FORMAL task is an execution specification, not a substitute for the Skill contract.

Before handing Codex a Skill behavior change:

```text
User + ChatGPT concept/design adjudication
→ governing concept/design updated
→ SKILL.md + references updated
→ committed task points to those exact Markdown owners
→ Codex implements/repairs code to conform
→ tests probe the general Skill contract
```

Codex MUST NOT create a task-specific production patch merely to satisfy one triggering example when the durable Skill contract is missing/ambiguous.

If local execution discovers a new design gap, classify/report `DESIGN_GAP` and stop the affected implementation path. Pure `IMPLEMENTATION_DRIFT` may proceed when the durable contract already determines expected behavior without interpretation.

## ChatGPT-first authoring

ChatGPT completes code/tests it can correctly author before handoff. Local verification need alone does not transfer all implementation authorship to Codex.

## Task-specific authority

The committed task file is the sole task-specific execution specification.

The User-facing response has:

```text
1. concise informational synopsis
2. copyable task locator
```

The synopsis MUST NOT introduce requirements absent from the committed task. If task semantics change, amend/supersede the task before repository-changing execution continues.

A User `STOP`, `PAUSE`, or `CANCEL` may take effect immediately.

## User-visible synopsis

After commit/push, provide approximately 8–12 short lines covering only high-level facts such as purpose, ChatGPT-authored state, why LOCAL work remains, main boundary, verification level, report path, and integration mode.

Do not dump commands, test matrices, retry logic, or acceptance tables into the synopsis.

## Copyable Codex launch block — hard UI requirement

After the synopsis, emit the complete launch prompt as a Markdown fenced code block whose opening fence is exactly:

````text
```text
````

and whose closing fence is exactly three backticks.

Do not use a blockquote/callout/writing block/list/inline code/ordinary paragraph or another fence language. Do not wrap the fence inside another container.

Exact block shape:

````text
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
````

The task URL uses the exact handoff commit. If the task was not successfully pushed, show `UNAVAILABLE — <blocker>` and do not represent the handoff as complete.

Do not append task-specific implementation detail after the code block.
