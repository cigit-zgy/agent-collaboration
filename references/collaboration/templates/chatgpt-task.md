# ChatGPT formal task template

Use this template only for the **formal delegated task** path defined in `../protocol.md`.

Routine local execution does not require a committed task/report ceremony.

Formal Codex tasks live at:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

A formal task is issued only after ChatGPT has:

1. identified the concrete local/unavailable capability that requires Codex;
2. partitioned every requested deliverable into `DIRECT` or `LOCAL`;
3. completed and committed/pushed all `DIRECT` deliverables that are in scope;
4. frozen those DIRECT artifacts as Codex read-only inputs;
5. reduced Codex scope to the remaining `LOCAL` work;
6. pinned the exact `agent-collaboration` GitHub authority used to author the task;
7. established the design/projection baseline commit from which the task is issued;
8. selected one verification level and a risk-based evidence-layer plan under `../verification.md`.

A task is invalid if it delegates a deliverable that ChatGPT can already complete through current connected capabilities without naming a concrete local-only dependency for that deliverable.

## Metadata

```yaml
---
artifact_type: chatgpt_task
task_id: <TASK_ID>
title: <SHORT_TITLE>
status: issued
date: <YYYY-MM-DD>
repository: <OWNER/REPOSITORY>
branch: <BRANCH>
baseline_sha: <DIRECT_DESIGN_PROJECTION_BASELINE_SHA>
verification_level: <level_1 | level_2 | level_3>
collaboration_repository: cigit-zgy/agent-collaboration
collaboration_commit: <PINNED_AGENT_COLLABORATION_SHA>
collaboration_entry: SKILL.md
summary: >
  <PURPOSE/SCOPE>
tags: []
concepts: []
codex_report: reports/codex/<YYMMDD_codex_NN.md>
---
```

`baseline_sha` is the commit after the task's DIRECT design/projection inputs are complete and before the formal task artifact is committed. It is **not** the execution handoff commit.

The task/handoff commit is the commit containing this task file. Because a file cannot contain the SHA of the commit that contains itself, the exact task/handoff commit is supplied in the launch block after the task has been committed and pushed.

The collaboration commit is required for formal tasks. Do not encode a machine-local `agent-collaboration` path as the authority source.

## Required body

```markdown
# <Task title>

## Mission

## Delegation partition

### ChatGPT-completed before handoff

<List every DIRECT deliverable completed before this task was issued, with paths/commits when relevant.>

### Frozen DIRECT inputs — Codex read-only

<List the exact files/directories Codex may read but MUST NOT substantively edit, delete, rename, reformat, regenerate, or replace.>

If local implementation exposes a defect in one of these artifacts, stop the affected work and report the conflict to ChatGPT. Do not repair the frozen artifact locally.

### Codex-owned local work

<For each LOCAL deliverable, state the concrete local/unavailable capability that makes Codex necessary.>

If a requested deliverable has no concrete local-only reason, it does not belong here.

## Why Codex is required

<Summarize the remaining local-only capability requirement after the partition.>

## Current evidence / diagnosed problem

## Authoritative sources

Identify project authorities normally, and identify collaboration authorities by pinned GitHub coordinates, for example:

```text
cigit-zgy/agent-collaboration@<PINNED_SHA>:SKILL.md
cigit-zgy/agent-collaboration@<PINNED_SHA>:references/collaboration/protocol.md
cigit-zgy/agent-collaboration@<PINNED_SHA>:references/collaboration/verification.md
cigit-zgy/agent-collaboration@<PINNED_SHA>:references/skill/writing.md
```

Codex resolves these exact files from GitHub unless an already-existing local checkout is verified to be the same repository at the same pinned commit. Do not substitute similarly named local files or another Skill.

## Scope
## Required changes
## Non-goals
## Upstream/downstream ownership boundary
## Scientific / product boundaries
## Engineering constraints
## Verification
## Acceptance criteria
## Git requirements
## Codex report
## Final stdout
```

## Partition rules

The task-level need for Codex does not grant Codex ownership of all files in the task area.

When ChatGPT has repository write access, substantive authoring of these artifacts is presumed `DIRECT` and should normally be completed before handoff:

```text
reports/concept/*.md
AGENTS.md
SKILL.md
references/*.md
substantive design/projection documentation
```

Codex consumes those artifacts as frozen authority/operational inputs.

Unless the task explicitly declares a narrowly mechanical exception, Codex must not modify any frozen DIRECT input. A discovered conflict is reported upward; it is not fixed by Codex through design/projection edits.

Codex may edit a normally `DIRECT` artifact only when the task states an inseparable local-only dependency, names the exact file and permitted transformation, and constrains the edit mechanically so that no new design semantics are introduced.

Examples of valid Codex-owned work:

```text
Python implementation
CLI behavior
packaging/import integration
local filesystem/worktree migration
focused/full tests
build/render/runtime verification
machine-local diagnostics
Codex execution report
```

Examples that should normally be completed by ChatGPT before handoff:

```text
canonical design decisions
AGENTS.md governance authoring
SKILL.md workflow authoring
references/*.md contract authoring
acceptance-criteria design
```

## Required upstream/downstream boundary statement

For a task that changes or re-establishes an upstream contract/stage, the task must state whether downstream migration is in scope.

Default wording when downstream migration is **not** in scope:

```text
Make the current owner conform to its frozen contract.
If downstream consumers still depend on the old contract, report the exact drift.
Do not modify those consumers, reintroduce rejected interfaces, or add compatibility
shims merely to make unrelated repository-wide tests pass.
```

Acceptance criteria should distinguish:

```text
current owner conformance
from
whole-pipeline compatibility
```

A focused stage can pass while explicit downstream drift remains, provided whole-pipeline migration was not promised by the task.

## Verification plan rules

The `verification_level` metadata chooses **how rigorous the task must be**. The `## Verification` body chooses **which evidence layers are required to support that claim**. These are separate axes; see `../verification.md`.

Every formal task must include an evidence-layer plan in `## Verification` using this form:

```text
Verification level: LEVEL 1 | LEVEL 2 | LEVEL 3

Evidence-layer plan:
- Layer 1 — Component/property: required | N/A — <concrete evidence or reason>
- Layer 2 — Contract/invariant: required | N/A — <concrete evidence or reason>
- Layer 3 — Integration: required | N/A — <concrete evidence or reason>
- Layer 4 — Real-artifact regression: required | N/A — <concrete evidence or reason>
- Layer 5 — E2E/recovery/repeatability: required | N/A — <concrete evidence or reason>
- Layer 6 — Release/non-functional: required | N/A — <concrete evidence or reason>
```

Rules:

- do not mark all six layers `required` mechanically;
- do not omit a material layer merely because focused pytest is green;
- use the lowest layer that proves a property, then add higher-layer evidence only for integration, real-artifact, end-to-end, recovery, repeatability, or release behavior;
- for LEVEL 3, every layer material to the release claim must be covered; genuinely irrelevant layers may be `N/A` with a reason;
- property/fuzz testing, coverage, mutation testing, fault injection, concurrency/race testing, and benchmarks are techniques within relevant layers, not standalone mandatory layers;
- when one of those techniques attacks a concrete task risk, name it explicitly in the layer plan and acceptance criteria.

The required evidence must be checkable. For example, write `real MinerU PDF smoke + inspect retained artifacts`, not merely `Layer 4 required`.

## Handoff and branch-freeze rules

Commit and push the formal task before handoff. The committed task source is Codex's execution specification.

The launch block must provide the exact task/handoff commit. Codex must reach and verify that commit before LOCAL implementation begins.

Once the User launches the task or Codex reports execution has begun, the handed-off branch is frozen for overlapping ChatGPT/User repository writes until Codex finishes or the task is explicitly aborted/superseded.

Do not advance the same branch with frozen-input or task-relevant changes during active Codex execution. If a DIRECT artifact must change, stop/supersede the task, commit the new DIRECT state, and issue a new coordinated handoff rather than forcing avoidable Git reconciliation.

Independent concurrent work belongs on a separate branch/worktree with proven non-interference.

Use the task-pinned `agent-collaboration` commit for collaboration/Git/concurrency/verification rules. Required changes and acceptance criteria should be directly checkable.

## Launch block

After the formal task is committed and pushed, give the User only this launch block rather than repeating the full specification:

```text
执行正式任务：

Repository:
<LOCAL_REPOSITORY>

Task:
reports/chatgpt/<TASK_FILE>.md

Task commit / execution handoff:
<TASK_COMMIT>

Collaboration authority:
cigit-zgy/agent-collaboration@<PINNED_AGENT_COLLABORATION_SHA>

先 fetch 并确认当前仓库状态、baseline 和 exact task/handoff commit。
安全同步到 task/handoff commit 后才开始实现。
严格执行 committed task，不依据聊天补充或扩大 scope。
需要 collaboration 规则时读取上面 pinned GitHub authority；不要用未验证的本地副本替代。
Frozen DIRECT inputs 对 Codex 只读；若实现发现矛盾，停止相关工作并报告，不要改写这些文件。
当前 handoff branch 在本任务执行期间视为冻结；若发现远端并发推进，不自行 merge/rebase/cherry-pick，按 protocol 停止并报告。
发现 out-of-scope downstream drift 时只报告，不自行迁移或加 compatibility shim。
按 task 的 verification level + evidence-layer plan 完成验证；不要用单一 pytest PASS 替代缺失的必需 Layer。
完成实现、规定验证、Codex report、commit 和 push。
最后输出 task 要求的固定 stdout。
```
