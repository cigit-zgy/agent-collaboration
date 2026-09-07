# FORMAL task, report, acceptance, and integration contract

Load this reference for committed FORMAL delegation, task/report binding, completion lookup, acceptance review, or post-acceptance integration.

Project report-family placement, canonical filenames, common metadata and archive rules are owned by `../project/reports.md`. Exact task/report body schemas and copyable UI blocks are owned by:

```text
templates/chatgpt-task.md
templates/codex-report.md
```

Do not load those templates unless creating/reviewing the corresponding artifact.

## Task authority

For a FORMAL task, the committed `reports/chatgpt/*.md` file is the sole task-specific execution specification. A chat synopsis or launch locator is navigation only and MUST NOT add, remove, reinterpret, or amend task semantics.

If task-specific requirements change after issue:

```text
update or supersede the committed task
→ commit/push revised specification
→ issue a new immutable handoff coordinate
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

Detailed local worktree/tmp/Git safety belongs to `execution.md`.

## Handoff coordinates

```text
baseline_sha
= task-branch commit after task-specific ChatGPT DIRECT inputs and before the task artifact

task/handoff commit
= commit containing the formal task; supplied in the launch locator
```

Before implementation, Codex verifies the exact task branch/handoff commit, pinned collaboration/project authorities, activated shared coding Skills, and frozen semantics.

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

The launch locator MUST be a Markdown fenced code block whose opening fence is exactly ` ```text ` so the UI exposes a Copy control. Exact content/format is owned by `templates/chatgpt-task.md`.

## Formal report

Codex writes the report at the exact `codex_report` path bound by the committed task and pushes it on the task branch. The report records implementation/execution evidence; it does not redefine design and is not final acceptance.

Exact metadata/body/result-locator requirements are owned by `templates/codex-report.md`.

## Acceptance review

Codex supplies evidence; ChatGPT performs acceptance review and issues:

```text
PASS | PASS WITH LIMITATIONS | BLOCKED | FAIL
```

Call this `acceptance review`, not independent review by default, because ChatGPT may also have designed, specified, or authored implementation. Use an additional independent model/reviewer/human perspective only when LEVEL 2/3 scientific, architectural, trust, security, or release risk materially warrants it.

The User retains final decision/override authority and designated human checkpoints.

## Completion shorthand and automatic report lookup

For the most recent relevant FORMAL handoff in the active project/conversation context, the User may simply say `Codex 已完成` or equivalent. ChatGPT resolves the most recent relevant FORMAL task, its expected Codex report, current remote task branch, task/report binding and evidence, then performs acceptance review.

Do not create a separate completion registry/status database.

## Post-acceptance integration

Every formal task declares:

```text
Post-acceptance integration: AUTO | USER_CHECKPOINT
```

`AUTO` authorizes connected mechanical remote integration after a permitting acceptance verdict. Use `USER_CHECKPOINT` only when integration itself is a genuine User decision such as release/publication authorization, destructive migration, unresolved scientific/product choice, repository visibility/licensing change, or another declared human checkpoint.

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

## Stable artifact paths and metadata

FORMAL artifacts use only:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
reports/codex/YYMMDD_codex_NN.md
```

Every artifact starts with the common metadata envelope from `../project/reports.md` plus the family-specific metadata required by its template. `artifact_id` equals the filename stem.

Issued artifacts remain historical evidence. Supersede; do not silently rewrite body semantics to match newer policy/state. Every FORMAL handoff/completion UI locator surfaces the corresponding repository artifact through a directly openable immutable HTTPS GitHub link.
