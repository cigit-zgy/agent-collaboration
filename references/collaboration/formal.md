# FORMAL task, report, acceptance, and integration contract

Load this reference for committed FORMAL delegation, task/report binding, completion lookup, acceptance review, or post-acceptance integration.

Exact task/report Markdown schemas and copyable UI blocks are owned by:

```text
templates/chatgpt-task.md
templates/codex-report.md
```

Do not load those templates unless creating/reviewing the corresponding artifact.

## Task authority

For a FORMAL task, the committed `reports/chatgpt/*.md` file is the sole task-specific execution specification.

A chat synopsis or launch locator is informational/navigation only. It MUST NOT add, remove, reinterpret, or amend task semantics.

If task-specific requirements change after issue:

```text
update or supersede the committed task
→ commit/push the revised specification
→ issue a new handoff commit
```

A User `STOP`, `PAUSE`, or `CANCEL` may take effect immediately. A substantive amendment must become durable before repository-changing execution continues.

## Default Git architecture

Repository-changing FORMAL work defaults to a dedicated task branch, normally with a dedicated local worktree when isolation is useful.

```text
default branch
→ task branch
→ task-specific ChatGPT DIRECT design/code/test inputs
→ formal task commit
→ Codex exact handoff
→ remaining local implementation/verification + report
→ push task branch
→ ChatGPT acceptance review
→ integration when permitted
```

Detailed local worktree/tmp/Git safety belongs to `execution.md`; `SKILL.md` names both owners when a FORMAL task also needs local execution mechanics.

The default branch may advance independently. Reconciliation at integration must follow permitted repository policy; conflicts are explicit and never hidden by destructive reset or force-push.

## Handoff coordinates

```text
baseline_sha
= task-branch commit after task-specific ChatGPT DIRECT inputs and before the task artifact

task/handoff commit
= commit containing the formal task; supplied in the launch locator
```

Before implementation, Codex must verify the exact task branch/handoff commit, pinned collaboration/project authorities, activated shared coding Skills, and frozen semantics.

## Skill-development FORMAL tasks

When a task changes maintained Skill behavior, the durable semantic order is:

```text
accepted concept/design
→ committed SKILL.md + references
→ FORMAL task points to those owners
→ Codex implements/repairs code to conform
```

The task is not a substitute for missing Skill semantics. If local execution exposes a design gap, Codex reports `DESIGN_GAP` and stops the affected implementation path rather than inventing task-local behavior.

## User-visible FORMAL handoff

The User-facing handoff has two layers:

```text
1. concise human-readable synopsis
2. copyable task locator
```

The synopsis is normally 8–12 short lines and remains substantially shorter than the task. Do not dump detailed commands, test matrices, retry logic, or acceptance tables into it.

The launch locator MUST be a Markdown fenced code block whose opening fence is exactly ` ```text ` so the ChatGPT UI exposes a direct Copy control. Exact content/format is owned by `templates/chatgpt-task.md`.

The locator includes the immutable task URL at the exact task/handoff commit. If the task is not pushed, report the publication blocker and do not fabricate a remote link.

## Formal report

Codex writes the report at the exact `codex_report` path bound by the committed task and pushes it on the task branch.

The report records implementation/execution evidence; it does not redefine design and is not final acceptance.

Exact metadata/body/result-locator requirements are owned by `templates/codex-report.md`.

## Acceptance review

Codex supplies evidence; ChatGPT performs acceptance review and issues:

```text
PASS | PASS WITH LIMITATIONS | BLOCKED | FAIL
```

Call this `acceptance review`, not independent review by default, because ChatGPT may also have designed, specified, or authored implementation.

Use an additional independent model/reviewer/human perspective only when LEVEL 2/3 scientific, architectural, trust, security, or release risk materially warrants it.

The User retains final decision/override authority and designated human checkpoints.

## Completion shorthand and automatic report lookup

For the most recent relevant FORMAL handoff in the active project/conversation context, the User may simply say:

```text
Codex 已完成
任务执行完了
```

ChatGPT resolves:

```text
most recent relevant FORMAL handoff
→ committed task at task/handoff commit
→ repository + task_branch + task_id + codex_report
→ current remote task branch
→ expected Codex report
→ task/report binding + commits/diff/evidence
→ acceptance review
```

Do not require the User to paste report URL/path/commit when the active context and repository can resolve them. Ask only when the intended task or required evidence is genuinely ambiguous/unavailable.

Do not create a separate completion registry/status database.

## Post-acceptance integration

Every formal task declares:

```text
Post-acceptance integration: AUTO | USER_CHECKPOINT
```

`AUTO` means ChatGPT should perform authorized mechanical remote integration after a permitting acceptance verdict when connected capability is sufficient, without another routine User confirmation.

Use `USER_CHECKPOINT` only when integration itself is a genuine User decision, such as:

```text
release/publication authorization
destructive migration
unresolved scientific/product choice
repository visibility/licensing change
another project-declared human checkpoint
```

If integration cannot be completed safely with available connected capability, report the concrete blocker and request only the minimum necessary action.

## Task lifecycle

Keep the lifecycle minimal:

```text
issued + handoff
→ one active execution owner
→ report / BLOCKED / FAIL
→ ChatGPT acceptance
→ permitted integration
```

An interrupted session may resume the same verified task branch when task semantics are unchanged. Semantic changes require a superseding task. Cancelled tasks receive no further task-attributed changes.

## Stable artifact paths

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
reports/codex/YYMMDD_codex_NN.md
```

Issued artifacts remain historical evidence. Supersede; do not silently rewrite them to match newer policy/state.

Every FORMAL handoff/completion UI locator surfaces the corresponding repository artifact through a directly openable immutable HTTPS GitHub link. A repository-relative path alone is insufficient.
