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
→ fresh-fetch + exact authorized-baseline synchronization
→ remaining local implementation/verification + report
→ push task branch
→ fresh-fetch + exact local/upstream equality verification
→ ChatGPT acceptance review
→ integration when permitted
```

Detailed local worktree/tmp/Git safety and the mandatory two-sided synchronization handshake belong to `execution.md`.

## Handoff coordinates

```text
baseline_sha
= exact authorized task-branch repository baseline after ChatGPT DIRECT inputs and before the task artifact

task/handoff commit
= commit containing the FORMAL task; supplied in the locator
```

Before any repository mutation, Codex fresh-fetches the remote and verifies the exact task branch/handoff coordinate, pinned collaboration/project authorities, activated shared coding Skills, and local execution baseline.

A stale local checkout is never an acceptable execution baseline. If fetched remote task state differs unexpectedly from the issued task coordinate/baseline, Codex stops rather than silently choosing a new baseline.

## Final publication boundary — hard requirement

Repository-changing FORMAL work is not complete merely because `git push` returns success.

Before reporting PASS/completion Codex MUST:

```text
commit task-scoped changes
→ push task branch
→ fresh-fetch remote refs again
→ resolve fetched upstream task-branch HEAD
→ prove local task HEAD == fetched upstream HEAD
→ record that evidence in the Codex report
```

If final local/upstream equality is not established, Codex MUST NOT report PASS.

Do not use blind `git pull`, destructive reset, rebase, stash, force checkout, or force push merely to synchronize local state.

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

For repository-changing work, the report must include the final fresh-fetch upstream equality evidence required by `execution.md`.

LOCAL-QUICK does not create a formal Codex report; that distinction is owned by `execution.md` and `templates/local-quick-task.md`.

## Acceptance review

Codex supplies evidence; ChatGPT performs acceptance review and issues:

```text
PASS | PASS WITH LIMITATIONS | BLOCKED | FAIL
```

Use an additional independent model/reviewer/human perspective only when LEVEL 2/3 scientific, architectural, trust, security, or release risk materially warrants it. The User retains final decision/override authority and designated human checkpoints.

## Completion shorthand and automatic report lookup

For the most recent relevant FORMAL task, the User may simply say `Codex 已完成`. ChatGPT resolves the expected report, current task branch, task/report binding, remote task-branch state, and evidence, then performs acceptance review.

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
→ pre-execution remote synchronization
→ local implementation/verification
→ report / BLOCKED / FAIL
→ pushed + post-push fresh-fetch equality
→ ChatGPT acceptance
→ permitted integration
```

An interrupted session may resume the same verified task branch when task semantics are unchanged, but before any new repository mutation it repeats the pre-execution remote synchronization handshake. Semantic changes require a superseding task.

## Stable artifact paths

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
reports/codex/YYMMDD_codex_NN.md
```

Every FORMAL artifact starts with the common metadata envelope from `../project/reports.md` plus its template-specific metadata. Issued artifacts remain historical evidence; supersede rather than silently rewriting semantics.
