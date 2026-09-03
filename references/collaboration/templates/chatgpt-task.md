# ChatGPT formal task template

Use this template only for the FORMAL route in `../protocol.md`.

LOCAL-QUICK work does not require a committed task/report ceremony.

Formal Codex tasks live at:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

## Before issuing

ChatGPT must have:

1. inspected current project/repository authority and evidence;
2. partitioned deliverables into DIRECT and LOCAL;
3. completed task-specific DIRECT work that can be completed through connected capability;
4. identified the semantic contracts/invariants Codex may not reinterpret;
5. reduced Codex scope to the remaining LOCAL implementation/execution;
6. selected a dedicated task branch unless the task explicitly justifies same-branch execution;
7. pinned the exact `agent-collaboration` commit used to author the task;
8. selected one verification level and concrete required evidence under `../verification.md`.

A formal task should remain small enough that its mission, implementation boundary, and acceptance claim can be reviewed coherently. Split independent responsibilities into separate tasks rather than using AI generation capacity to create one oversized task.

## Metadata

```yaml
---
artifact_type: chatgpt_task
task_id: <TASK_ID>
title: <SHORT_TITLE>
status: issued
date: <YYYY-MM-DD>
repository: <OWNER/REPOSITORY>
task_branch: <DEDICATED_TASK_BRANCH>
baseline_sha: <DIRECT_TASK_BASELINE_SHA>
verification_level: <level_1 | level_2 | level_3>
collaboration_commit: <PINNED_AGENT_COLLABORATION_SHA>
summary: >
  <PURPOSE/SCOPE>
codex_report: reports/codex/<YYMMDD_codex_NN.md>
---
```

`baseline_sha` is the task-branch commit after task-specific DIRECT inputs are complete and before the task artifact is added.

The task/handoff commit is the commit containing this task file. Because a file cannot contain its own SHA, provide that SHA in the launch block after committing/pushing the task.

## Required body

Use the smallest body that makes the implementation boundary auditable:

```markdown
# <Task title>

## Mission

## Authority and frozen semantics

<Project authority + exact design/operational contracts Codex must implement without reinterpretation.>

Pinned collaboration authority:

- cigit-zgy/agent-collaboration@<SHA>:SKILL.md
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/protocol.md
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/implementation.md
- cigit-zgy/agent-collaboration@<SHA>:references/collaboration/verification.md

## LOCAL scope

<What Codex owns and the concrete local/runtime capability that makes it LOCAL.>

## Required changes

## Non-goals / ownership boundary

## Engineering and AI-implementation constraints

## Acceptance criteria

## Verification

Verification level: LEVEL 1 | LEVEL 2 | LEVEL 3

Required evidence:
- <category>: <concrete check/evidence>
- ...

## Git handoff and integration

## Codex report
```

Omit a subsection only when its information is genuinely inapplicable; do not replace omitted substance with boilerplate.

## Authority and semantic-freeze rules

Codex may read all relevant authority but must not reinterpret accepted scientific/product/design semantics.

Freeze the named semantic contracts/invariants rather than every DIRECT file by default.

If local implementation reveals a conflict in a frozen semantic contract:

```text
stop affected work
→ report exact conflict
→ do not silently redesign
```

A mechanical projection correction is allowed only when the task explicitly defines the permitted class of change and it cannot introduce new design semantics.

For an upstream-stage task where downstream migration is not in scope, state concisely:

```text
Make the current owner conform to its accepted contract.
Report stale downstream consumers precisely.
Do not restore rejected upstream interfaces or add compatibility shims merely to make unrelated tests pass.
```

## Engineering and AI-transparency rules

Every implementation task is governed by `../implementation.md`.

Acceptance should require, when material:

```text
smallest sufficient implementation
existing patterns/mature tools before new infrastructure
bounded/reviewable logical change
no speculative abstraction/dependency/compatibility layer
same quality standard for AI-produced and human-produced code
implementation rationale and limitations in the Codex result/report
```

Project mechanical style remains owned by project tooling/CI rather than repeated in prose.

## Verification plan rules

The metadata chooses the verification level. The body lists only evidence categories actually required to establish the claim.

Do not include a mandatory six-row `required | N/A` matrix.

Examples:

```text
Verification level: LEVEL 2

Required evidence:
- Contract / invariant: registry schema and fail-closed path checks
- Integration: CLI → registry consumer handoff
- Real artifact / external tool: one real scientific PDF through the parser
- E2E / recovery / repeatability: parser failure leaves no partial final state and retry succeeds
```

Techniques such as coverage, fuzzing, mutation testing, fault injection, concurrency testing, or benchmarking are named only when they attack a concrete risk.

## Task branch and integration

Repository-changing FORMAL work defaults to a dedicated task branch/worktree.

The task branch is the active execution boundary. The default branch may continue independently when mutable resources do not interfere.

Codex verifies and pushes the task branch; ChatGPT performs acceptance review before integration.

If the default branch advances during execution, that is not by itself a task failure. Reconcile once at integration using the repository's permitted fast-forward/merge/PR policy. Conflicts or design changes remain explicit decisions.

Same-branch formal execution is an exception and must be named in the task with its concurrency constraints.

## Launch block

After the task is committed and pushed, give the User a compact launch block:

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
安全到达 exact task branch + handoff commit 后才开始实现。
严格执行 committed task，不依据聊天扩大 scope。
需要 collaboration 规则时读取 pinned GitHub authority，不用未验证的本地副本替代。
冻结的是 task 明确列出的 design semantics / contracts；发现设计冲突时停止相关实现并报告，不自行改写语义。
代码实现遵循 implementation.md：最小充分实现、可审查增量、AI 代码与人工代码同一质量标准，并在 report 中说明关键实现理由与限制。
按 task 的 verification level + required evidence 完成验证，不用单一 pytest PASS 替代其他必需证据。
完成实现、验证、Codex report、task-scoped commit 和 task-branch push。
ChatGPT acceptance review 后再集成 default branch。
```
