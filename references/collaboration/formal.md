# FORMAL task, report, acceptance, and integration contract

Load this reference for committed FORMAL delegation, task/report binding, completion lookup, acceptance review, or post-acceptance integration.

All Codex repository tasks first use a committed `reports/chatgpt/` task artifact under `execution.md`. FORMAL additionally requires a bound `reports/codex/` report.

Exact FORMAL task/report body schemas and UI locators are owned by:

```text
templates/chatgpt-task.md
templates/codex-report.md
```

Do not load those templates unless creating/reviewing the corresponding artifact.

## Task authority

For FORMAL work, the committed `reports/chatgpt/*.md` file is the sole task-specific execution specification. Chat content is navigation only and MUST NOT add, remove, reinterpret, summarize in detail, or amend task semantics.

If task-specific requirements change after issue:

```text
update or supersede committed task
→ commit/push revised specification
→ issue new immutable locator
```

A User `STOP`, `PAUSE`, or `CANCEL` may take effect immediately. A substantive amendment becomes durable before repository-changing execution continues.

## Default Git architecture

Repository-changing FORMAL work defaults to a dedicated task branch, normally with a linked worktree when isolation is useful.

```text
default branch
→ task branch
→ ChatGPT DIRECT design/code/test inputs
→ FORMAL task commit
→ short Codex locator
→ remaining local implementation/verification + report
→ push task branch
→ ChatGPT acceptance review
→ integration when permitted
```

Detailed local worktree/tmp/Git safety belongs to `execution.md`.

## Handoff coordinates

```text
baseline_sha
= task-branch commit after ChatGPT DIRECT inputs and before the task artifact

task/handoff commit
= commit containing the FORMAL task; supplied in the locator
```

Before implementation, Codex verifies the exact task branch/handoff commit, pinned collaboration/project authorities, activated shared coding Skills, and frozen semantics from the task.

## Skill-development FORMAL tasks

When a task changes maintained Skill behavior:

```text
current accepted design
→ committed SKILL.md + references
→ FORMAL task points to those owners
→ Codex implements/repairs code to conform
```

The task is not a substitute for missing Skill semantics. A local design gap is reported as `DESIGN_GAP`; Codex stops the affected path rather than inventing task-local behavior.

## User-visible FORMAL handoff — hard boundary

The User-facing handoff is intentionally minimal:

```text
optional one short sentence
+ one copyable task locator
```

There is no required 8–12-line synopsis. Do not restate the task body for convenience.

The launch locator MUST be a fenced `text` block and contain only repository/task coordinates plus the immutable task link and authority sentence. Exact format is owned by `templates/chatgpt-task.md`.

If more task detail seems necessary in chat, the committed task is insufficient: fix the task artifact instead of expanding the chat prompt.

## Formal report

Codex writes the report at the exact `codex_report` path bound by the committed task and pushes it on the task branch. The report records implementation/execution evidence; it does not redefine design and is not final acceptance.

LOCAL-QUICK does not create a formal Codex report; that distinction is owned by `execution.md` and `templates/local-quick-task.md`.

## Acceptance review

Codex supplies evidence; ChatGPT performs acceptance review and issues:

```text
PASS | PASS WITH LIMITATIONS | BLOCKED | FAIL
```

Use an additional independent model/reviewer/human perspective only when LEVEL 2/3 scientific, architectural, trust, security, or release risk materially warrants it. The User retains final decision/override authority and designated human checkpoints.

## Completion shorthand and automatic report lookup

For the most recent relevant FORMAL task, the User may simply say `Codex 已完成`. ChatGPT resolves the expected report, current task branch, task/report binding, and evidence, then performs acceptance review.

Do not create a separate completion registry/status database.

## Post-acceptance integration

Every FORMAL task declares:

```text
Post-acceptance integration: AUTO | USER_CHECKPOINT
```

`AUTO` authorizes connected mechanical remote integration after a permitting acceptance verdict. Use `USER_CHECKPOINT` only when integration itself is a genuine User decision such as release/publication authorization, destructive migration, unresolved scientific/product choice, repository visibility/licensing change, or another declared checkpoint.

## Task lifecycle

```text
issued + locator
→ one active execution owner
→ report / BLOCKED / FAIL
→ ChatGPT acceptance
→ permitted integration
```

An interrupted session may resume the same verified task branch when task semantics are unchanged. Semantic changes require a superseding task.

## Stable artifact paths

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
reports/codex/YYMMDD_codex_NN.md
```

Every FORMAL artifact starts with the common metadata envelope from `../project/reports.md` plus its template-specific metadata. Issued artifacts remain historical evidence; supersede rather than silently rewriting semantics.
