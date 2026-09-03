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

`baseline_sha` is the task-branch commit after task-specific DIRECT inputs and before the task artifact. Supply the commit containing the task separately in the launch envelope as the execution handoff.

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

## Task specification authority — hard requirement

The committed task file is the **sole task-specific execution specification** for a FORMAL handoff.

The User-facing launch message is only a transport/locator envelope. It MUST NOT duplicate, summarize, paraphrase, expand, or amend task semantics.

The launch envelope MUST NOT contain any of the following task-specific content:

```text
mission or diagnosed problem
scientific/product/design semantics
required changes or non-goals
validator/error-specific behavior
implementation instructions
verification commands or test matrix
acceptance criteria
recovery/retry semantics
Git procedure already owned by the pinned collaboration contract
custom final-stdout schema
```

All such information belongs in the committed task and, after execution, in the Codex report.

If any task-specific requirement must change after the task is committed, update or supersede the task, commit/push the revised specification, and issue a new handoff commit. Do not append a second specification in chat.

A chat-only emergency `STOP`, `PAUSE`, or `CANCEL` from the User may take effect immediately. A substantive amendment must be made durable in the task before repository-changing execution continues.

## User-visible task link — hard requirement

After the formal task is committed and pushed, ChatGPT MUST surface a directly openable immutable link to the exact committed task:

```text
任务链接如下：
https://github.com/<OWNER>/<REPOSITORY>/blob/<TASK_COMMIT>/reports/chatgpt/<TASK_FILE>.md
```

`<TASK_COMMIT>` is the execution handoff commit that contains the task. Use the full HTTPS GitHub URL, not only the repository-relative path or commit SHA.

If the task was not successfully pushed, do not fabricate the link. Show `任务链接如下：UNAVAILABLE — <blocker>` and do not represent the FORMAL handoff as complete.

## Launch envelope — exact fixed format

After committing/pushing the task, give the User **only** the following launch envelope. Do not add task semantics before or after it.

```text
执行正式任务：
Repository: <LOCAL_REPOSITORY>
Task: reports/chatgpt/<TASK_FILE>.md
Task branch: <TASK_BRANCH>
Task commit: <TASK_COMMIT>
Collaboration: cigit-zgy/agent-collaboration@<PINNED_AGENT_COLLABORATION_SHA>
任务链接如下：
https://github.com/<OWNER>/<REPOSITORY>/blob/<TASK_COMMIT>/reports/chatgpt/<TASK_FILE>.md
```

This fixed envelope is intentionally short. Its only purpose is to locate and bind the durable specification. The task file and pinned collaboration authority contain the execution rules.

A FORMAL handoff that repeats task-specific semantics outside this envelope is non-conforming, even when the repeated text is identical to the committed task.
