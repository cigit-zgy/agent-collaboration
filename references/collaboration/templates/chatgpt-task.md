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
4. reduced Codex scope to the remaining `LOCAL` work;
5. pinned the exact `agent-collaboration` GitHub authority used to author the task.

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
baseline_sha: <BASELINE_SHA>
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

The collaboration commit is required for formal tasks. Do not encode a machine-local `agent-collaboration` path as the authority source.

## Required body

```markdown
# <Task title>

## Mission

## Delegation partition

### ChatGPT-completed before handoff

<List every DIRECT deliverable completed before this task was issued, with paths/commits when relevant.>

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

Codex may consume those artifacts as frozen authority/operational inputs.

Codex may edit a normally `DIRECT` artifact only when the task states an inseparable local-only dependency and constrains the edit mechanically so that no new design semantics are introduced.

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

Use the task-pinned `agent-collaboration` commit for collaboration/Git/concurrency/verification rules. Required changes and acceptance criteria should be directly checkable.

Commit and push the formal task before handoff; the committed task source is Codex's execution specification.

## Launch block

After the formal task is committed and pushed, give the User only this launch block rather than repeating the full specification:

```text
执行正式任务：

Repository:
<LOCAL_REPOSITORY>

Task:
reports/chatgpt/<TASK_FILE>.md

Task commit:
<TASK_COMMIT>

Collaboration authority:
cigit-zgy/agent-collaboration@<PINNED_AGENT_COLLABORATION_SHA>

先 fetch 并确认当前仓库状态和 baseline。
严格执行 committed task，不依据聊天补充或扩大 scope。
需要 collaboration 规则时读取上面 pinned GitHub authority；不要用未验证的本地副本替代。
完成实现、规定验证、Codex report、commit 和 push。
最后输出 task 要求的固定 stdout。
```
