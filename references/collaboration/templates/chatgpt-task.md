# ChatGPT formal task template

Use only for the FORMAL route in `../protocol.md`. LOCAL-QUICK does not require a committed task/report.

Formal tasks live at:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

## Before issuing

ChatGPT must have:

```text
refreshed current collaboration authority for this new repository-changing work unit
→ inspected current project authority/evidence
→ partitioned authoring and verification separately
→ completed task-specific DIRECT design and code/test authoring it can perform
→ resolved the shared coding-Skill profile and activated Skill authorities
→ identified frozen semantic contracts/invariants
→ selected a dedicated task branch unless explicitly excepted
→ pinned the verified collaboration commit
→ selected verification level + concrete remaining evidence
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
coding_skill_profile: >
  cigit-zgy/agent-collaboration@<PINNED_AGENT_COLLABORATION_SHA>:
  references/collaboration/shared-coding-skills.md
summary: >
  <PURPOSE/SCOPE>
codex_report: reports/codex/<YYMMDD_codex_NN.md>
---
```

`baseline_sha` is the task-branch commit after task-specific DIRECT design/authoring inputs and before the task artifact. Supply the commit containing the task separately in the launch prompt as the execution handoff.

`coding_skill_profile` binds the cross-Agent coding rules used by ChatGPT and Codex. Additional project/task-specific Skill authorities are stated in the body using immutable repository/commit/path coordinates.

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
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/shared-coding-skills.md
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/verification.md
- cigit-zgy/agent-collaboration@<SHA>:references/project/architecture.md
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/templates/codex-report.md

<Frozen scientific/product/design contracts Codex must not reinterpret.>

## Shared coding Skills and authoring state

Shared profile:
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/shared-coding-skills.md

Activated shared Skills:
- <SKILL_NAME> — <MODE/ACTIVATION>

Additional project/task Skill authorities:
- <NONE OR OWNER/REPO@COMMIT:PATH/TO/SKILL.md — ACTIVATION/MODE>

ChatGPT-authored before handoff:
- <IMPLEMENTATION/TEST PATHS OR NONE + REASON>

ChatGPT checks already completed:
- <CHECK + RESULT OR NONE>

Remaining Codex-local work:
- <LOCAL VERIFICATION, BOUNDED REPAIR, OR LOCAL-FEEDBACK-DEPENDENT IMPLEMENTATION>

## LOCAL scope

<What Codex owns and why local/runtime capability is required. Do not delegate code authoring merely because final verification is local.>

## Required changes

## Non-goals / ownership boundary

## Engineering constraints

<Only task-specific constraints. General AI implementation policy comes from implementation.md; cross-Agent coding rules come from shared-coding-skills.md; project-local temporary-state rules come from project/architecture.md; mechanical style comes from project tooling.>

## Acceptance criteria

## Verification

Verification level: LEVEL 1 | LEVEL 2 | LEVEL 3

ChatGPT checks already completed:
- <check>: <result>

Remaining Codex-local evidence:
- <category>: <concrete check>
- ...

Shared coding-Skill alignment:
- verify every activated Skill against the task-pinned profile before local code work

Temporary-state closure:
- temporary workspace cleaned, or exact retained recovery state + reason reported

## Git handoff / integration

Task branch: <TASK_BRANCH>
Target integration branch: <TARGET_BRANCH>
Post-acceptance integration: AUTO | USER_CHECKPOINT
Local temporary workspace: <PROJECT_ROOT>/tmp/<TASK_ID>/
<Any explicitly User-authorized temporary-path exception, same-branch exception, or repository-specific integration condition.>

## Codex report

reports/codex/<YYMMDD_codex_NN.md>
```

List only verification categories actually required; no mandatory `N/A` matrix.

Do not repeat a check ChatGPT already completed unless rerunning it is required against Codex's final branch state or supplies a distinct local-environment claim.

For an upstream owner where downstream migration is out of scope, the task should state that stale consumers are reported rather than repaired and rejected upstream interfaces are not restored for compatibility.

A narrowly mechanical projection edit is permitted only when the task names that permission and it cannot alter frozen semantics. A design conflict stops the affected implementation for User + ChatGPT adjudication.

### ChatGPT-first authoring rule

ChatGPT completes code/tests it can correctly author from repository content, accepted design, project tooling, and the shared coding-Skill authorities before handoff.

The task may delegate initial code authorship to Codex only when an iterative local feedback loop is materially required for correctness. Name that dependency concretely.

ChatGPT-authored code is not frozen merely because ChatGPT wrote it. Codex may make bounded implementation repairs supported by local evidence, while frozen scientific/product/design semantics remain unchanged.

### Shared coding-Skill alignment rule

At task start, Codex checks only the activated Skills listed above.

```text
exact local revision/path match
→ use local content

mismatch with readable pinned source
→ use the pinned source as authority

local scripts/assets required
→ align a clean local cache to the exact pinned revision when safely authorized

unresolvable or dirty/conflicting source
→ report/block rather than silently use another revision
```

Do not update all installed Skills and do not adopt upstream latest during a running task. See `../shared-coding-skills.md`.

### Local temporary-state rule

Unless the User explicitly authorizes another location, all Agent-created local scratch state for the task is confined to:

```text
<PROJECT_ROOT>/tmp/<TASK_ID>/
```

This includes linked worktrees, scratch/test/E2E outputs, downloads, renders, caches, intermediates, and disposable environments. Do not create sibling project worktrees or Desktop/Documents-root test folders.

At completion, clean temporary state that has no recovery value. Preserve dirty, unpushed, active, or ambiguous state. Git linked worktrees must be removed with Git-aware worktree commands rather than blind filesystem deletion. The owning rules are in `../protocol.md` and `../../project/architecture.md`.

A housekeeping task may explicitly authorize cleanup of legacy Agent-created state outside the current project `tmp/` boundary. Such an exception must name the cleanup scope and preserve canonical project/source directories.

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
what ChatGPT already authored
why remaining LOCAL/Codex execution is needed
activated shared coding Skills
main frozen boundary or important non-goal
verification level / major remaining evidence
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

以 committed task 为唯一 task-specific 执行规范；使用 pinned collaboration、shared coding-Skill profile 和 project authority 执行实现与验证。
```

Do not append task-specific implementation detail after the code block. The surrounding synopsis may explain the task at high level, but the boxed prompt must not become a second detailed specification.

A FORMAL handoff is non-conforming when any of these occurs:

- no 8–12-line concise synopsis is provided without a concrete reason;
- the boxed prompt contains substantive task-specific requirements that belong in the committed task;
- a material coding Skill is referenced only by a local path/name rather than a shared immutable authority;
- all implementation is delegated solely because remaining verification requires the local environment;
- Agent-created local temporary state is intentionally placed outside the project `tmp/` boundary without an explicit User-authorized exception.
