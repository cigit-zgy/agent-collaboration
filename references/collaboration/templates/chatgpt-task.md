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

`baseline_sha` is the task-branch commit after task-specific DIRECT inputs and before the task artifact. Supply the commit containing the task separately in the launch prompt as the execution handoff.

`codex_report` is the canonical expected report destination for this task. Codex MUST write the formal report at exactly that repository-relative path and push it on `task_branch`. Do not choose a different report filename/path after handoff unless the task is durably amended or superseded.

This binding exists so ChatGPT can locate the report automatically from the committed task without requiring the User to paste a report URL or path after Codex finishes.

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

Task branch: <TASK_BRANCH>
Target integration branch: <TARGET_BRANCH>
Post-acceptance integration: AUTO | USER_CHECKPOINT
<Any same-branch exception or repository-specific integration condition.>

## Codex report

reports/codex/<YYMMDD_codex_NN.md>
```

List only verification categories actually required; no mandatory `N/A` matrix.

For an upstream owner where downstream migration is out of scope, the task should state that stale consumers are reported rather than repaired and rejected upstream interfaces are not restored for compatibility.

A narrowly mechanical projection edit is permitted only when the task names that permission and it cannot alter frozen semantics. A design conflict stops the affected implementation for User + ChatGPT adjudication.

### Post-acceptance integration policy

Use `AUTO` when the User has already accepted the governing design/task intent and integration is a mechanical repository operation with no new scientific/product/trust/release/destructive decision. `AUTO` is preferred for ordinary implementation tasks to avoid an unnecessary extra User confirmation.

Use `USER_CHECKPOINT` when integration itself is a genuine human decision, for example publication/release authorization, destructive migration, externally visible product behavior, unresolved scientific choice, repository visibility/licensing change, or another project-declared checkpoint.

When `AUTO` is declared and ChatGPT's acceptance verdict is `PASS` (or `PASS WITH LIMITATIONS` only when the task explicitly permits integration with those limitations), ChatGPT SHOULD perform the permitted remote integration with available connected repository tools and verify the resulting remote state without asking the User for another routine confirmation.

If safe integration requires an unavailable local capability or non-trivial reconciliation not authorized by the task, report that concrete blocker instead of silently expanding authority.

## Task specification authority — hard requirement

The committed task file is the **sole task-specific execution specification** for a FORMAL handoff.

The User-facing response has two layers:

```text
1. concise human-readable synopsis
2. boxed formal launch prompt
```

The synopsis is informational only. It may summarize the committed task, but it MUST NOT add, remove, reinterpret, or amend task semantics. If the synopsis and committed task differ, the committed task is authoritative.

If any task-specific requirement must change after the task is committed, update or supersede the task, commit/push the revised specification, and issue a new handoff commit. Do not create a second specification in chat.

A chat-only emergency `STOP`, `PAUSE`, or `CANCEL` from the User may take effect immediately. A substantive amendment must be made durable in the task before repository-changing execution continues.

## User-visible synopsis — hard requirement

After the task is committed and pushed, ChatGPT MUST provide a short synopsis of approximately ten lines before the formal launch prompt.

Normal conformance target:

```text
8–12 short lines
```

Each line should communicate at most one high-level fact. The synopsis should normally cover only the most useful items, for example:

```text
task purpose
main affected component or workflow
why LOCAL/Codex execution is needed
main frozen boundary or important non-goal
high-level implementation direction
verification level / major evidence category
expected stable result
expected Codex report path
post-acceptance integration mode
```

The synopsis MUST remain substantially shorter than the committed task. It MUST NOT reproduce detailed validator/error strings, command lists, test matrices, retry/recovery state machines, field-by-field acceptance criteria, long prohibitions, custom final-stdout schemas, or other low-level execution instructions.

The synopsis is allowed to summarize those concerns at a high level when that helps the User understand the task. Summary is not specification.

## User-visible task link — hard requirement

The formal launch prompt MUST include a directly openable immutable link to the exact committed task:

```text
任务链接如下：
https://github.com/<OWNER>/<REPOSITORY>/blob/<TASK_COMMIT>/reports/chatgpt/<TASK_FILE>.md
```

`<TASK_COMMIT>` is the execution handoff commit that contains the task. Use the full HTTPS GitHub URL, not only the repository-relative path or commit SHA.

If the task was not successfully pushed, do not fabricate the link. Show `任务链接如下：UNAVAILABLE — <blocker>` and do not represent the FORMAL handoff as complete.

## Formal launch prompt — boxed exact format

After the synopsis, ChatGPT MUST place the complete copyable Codex launch prompt in one fenced plain-text code block. The prompt itself stays intentionally short and contains only durable coordinates plus one authority sentence:

```text
执行正式任务：

Repository: <LOCAL_REPOSITORY>
Task: reports/chatgpt/<TASK_FILE>.md
Task branch: <TASK_BRANCH>
Task commit: <TASK_COMMIT>
Collaboration: cigit-zgy/agent-collaboration@<PINNED_AGENT_COLLABORATION_SHA>

任务链接如下：
https://github.com/<OWNER>/<REPOSITORY>/blob/<TASK_COMMIT>/reports/chatgpt/<TASK_FILE>.md

以 committed task 为唯一 task-specific 执行规范；使用 pinned collaboration authority 执行协作、Git、实现与验证规则。
```

Do not append task-specific implementation detail after the code block. The surrounding synopsis may explain the task at high level, but the boxed prompt must not become a second detailed specification.

A FORMAL handoff is non-conforming when either of these occurs:

- no 8–12-line concise synopsis is provided without a concrete reason;
- the boxed prompt contains substantive task-specific requirements that belong in the committed task.
