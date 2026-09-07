# ChatGPT formal task template

Use only for the FORMAL route in `../protocol.md`. LOCAL-QUICK does not require a committed task/report.

Formal tasks live at:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

## Before issuing

ChatGPT must have:

```text
refreshed current collaboration authority for this repository-changing work unit
→ inspected current project/design authority and repository state
→ completed DIRECT design / Markdown projection / code / tests it can correctly author
→ for Skill work, applied references/skill/development.md
→ resolved activated shared coding-Skill authorities
→ identified frozen semantics and genuine remaining LOCAL work
→ selected task branch + verification level
→ pinned collaboration and task authority
```

Keep one formal task to one reviewable logical responsibility.

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

`baseline_sha` is the task-branch commit after ChatGPT's task-specific DIRECT authoring and before the task artifact.

`codex_report` is the canonical expected report path. Codex MUST use it exactly unless the task is durably superseded/amended.

## Body

Use the smallest body that makes the LOCAL work deterministic:

```markdown
# <Task title>

## Mission

## Authority and frozen semantics

Project/design authority:
- <governing concept/design files>

Operational authority:
- <governing SKILL.md / references when applicable>

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
- <NONE OR OWNER/REPO@COMMIT:PATH — ACTIVATION/MODE>

ChatGPT-authored before handoff:
- <CONCEPT / SKILL MARKDOWN / IMPLEMENTATION / TEST PATHS OR NONE + REASON>

ChatGPT checks already completed:
- <CHECK + RESULT OR NONE>

Remaining Codex-local work:
- <LOCAL VERIFICATION, BOUNDED REPAIR, OR LOCAL-FEEDBACK-DEPENDENT IMPLEMENTATION>

## LOCAL scope

## Required changes

## Non-goals / ownership boundary

## Engineering constraints

## Acceptance criteria

## Verification

Verification level: LEVEL 1 | LEVEL 2 | LEVEL 3

ChatGPT checks already completed:
- <check>: <result>

Remaining Codex-local evidence:
- <category>: <concrete check>

Shared coding-Skill alignment:
- verify every activated Skill against the task-pinned profile

Temporary-state closure:
- temporary workspace cleaned, or exact retained recovery state + reason reported

## Git handoff / integration

Task branch: <TASK_BRANCH>
Target integration branch: <TARGET_BRANCH>
Post-acceptance integration: AUTO | USER_CHECKPOINT
Local temporary workspace: <PROJECT_ROOT>/tmp/<TASK_ID>/

## Codex report

reports/codex/<YYMMDD_codex_NN.md>
```

List only evidence categories actually needed. Do not create an `N/A` matrix.

## Skill-development task — hard requirement

When a FORMAL task touches a maintained first-party Skill, apply `../../skill/development.md`.

If the task changes or questions Skill semantics, workflow, routing, state, trust, recovery, completion, or public behavior:

```text
User + ChatGPT concept/design adjudication
→ governing concept/design updated
→ SKILL.md + references updated
→ committed task points to those exact Markdown owners
→ Codex implements/repairs code to conform
→ tests probe the general Skill contract
```

The task file is an execution specification. It MUST NOT be the sole owner of new Skill semantics.

Codex MUST NOT make a task-specific code patch merely to satisfy the triggering example/test when the durable Skill contract is missing or ambiguous.

If Codex discovers a new design gap:

```text
stop affected implementation path
→ classify/report DESIGN_GAP
→ return to User + ChatGPT
```

If concept + Skill Markdown already determine the expected behavior without interpretation, a pure `IMPLEMENTATION_DRIFT` repair may proceed without unnecessary concept edits.

Testing of a Skill is aimed at finding design/contract insufficiency and generality failures, not maximizing one task fixture. A task-specific regression test is valid only when it encodes a general accepted invariant.

## ChatGPT-first authoring

ChatGPT completes code/tests it can correctly author from repository content, accepted design, project tooling, and shared coding-Skill authorities before handoff.

Do not delegate all implementation merely because final verification is local. Codex becomes primary implementation author only when correctness materially requires a local feedback loop unavailable to ChatGPT.

## Shared coding-Skill alignment

At task start, Codex checks only activated Skills:

```text
exact local revision/path match
→ use local content

mismatch + readable pinned source
→ use pinned source as authority

local scripts/assets required
→ safely align a clean cache to the exact pin when authorized

unresolvable / dirty / conflicting
→ report or block; never silently substitute another revision
```

Do not update all installed Skills or adopt upstream latest during a running task.

## Local temporary-state boundary

Unless the User explicitly authorizes another location, Agent-created local scratch state is confined to:

```text
<PROJECT_ROOT>/tmp/<TASK_ID>/
```

This includes linked worktrees, test/E2E outputs, downloads, renders, caches, intermediates, and disposable environments.

Do not create sibling project worktrees or Desktop/Documents-root test folders. Clean temporary state with no recovery value at completion. Remove linked worktrees through Git-aware worktree operations.

## Post-acceptance integration

Use `AUTO` for mechanical integration after an accepted ordinary implementation task.

Use `USER_CHECKPOINT` only when integration itself requires a genuine User decision, such as release/publication authorization, destructive migration, unresolved scientific/product choice, repository visibility/licensing, or another declared checkpoint.

## Task specification authority — hard requirement

The committed task file is the sole task-specific execution specification.

The User-facing handoff has exactly two semantic layers:

```text
1. concise informational synopsis
2. copyable task locator
```

The synopsis MUST NOT introduce task requirements absent from the committed task.

If task semantics change, amend/supersede the committed task before repository-changing execution continues.

## User-visible synopsis

After the task is committed/pushed, provide approximately 8–12 short lines summarizing only high-level facts such as purpose, what ChatGPT already authored, why LOCAL execution remains, main boundary, verification level, report path, and integration mode.

Do not dump command lists, test matrices, retry logic, or acceptance tables into the synopsis.

## Copyable Codex launch block — hard UI requirement

After the synopsis, the complete Codex launch prompt MUST be emitted as a Markdown fenced code block whose opening fence is **exactly**:

````text
```text
````

and whose closing fence is exactly three backticks.

This requirement exists so the ChatGPT UI renders a code block with a direct **Copy** control.

MUST NOT use any of these for the launch prompt:

```text
Markdown blockquote lines beginning with >
callout / quote / citation block
writing block
bulleted or numbered list
inline code
ordinary paragraph text
another fence language such as markdown, yaml, bash, shell, or plaintext
```

Do not wrap the `text` fence inside another quote/callout/container.

The content inside the block is exactly this shape:

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

The task link must be an immutable HTTPS link to the exact task-containing commit. If the task was not pushed, show `UNAVAILABLE — <blocker>` and do not claim the handoff is complete.

Do not append task-specific implementation instructions after the fenced block.

A FORMAL handoff is non-conforming when:

- the launch prompt is not in the exact `text` fenced code block;
- no concise synopsis is provided without a concrete reason;
- the launch block carries new task semantics not present in the committed task;
- a material coding Skill is referenced only by local name/path instead of immutable authority;
- Skill behavior is implemented from task prose while concept/Skill Markdown remains ambiguous;
- all implementation is delegated solely because final verification is local;
- local temporary state is deliberately placed outside project `tmp/` without explicit User authorization.
