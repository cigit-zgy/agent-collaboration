# FORMAL task, report, acceptance, and integration contract

Load this reference for FORMAL delegation, task/report binding, acceptance review, Design synchronization, or post-acceptance integration.

FORMAL uses:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
reports/codex/YYMMDD_codex_NN.md
```

Exact artifact templates are cold and loaded only when creating/reviewing those files.

## When FORMAL is appropriate

Use FORMAL when the work has material architectural, scientific/product, trust, destructive/shared-state, security, release, reproducibility, or long-running execution risk that benefits from a richer durable execution record.

Do not choose FORMAL merely because a task is large in line count.

## Task authority

The committed `reports/chatgpt/` task is the sole task-specific execution specification. Chat is only a locator.

A good task defines:

```text
Mission / intended outcome
Authority and frozen boundaries
Scope / material non-goals
Mutation scope / concurrency keys for repository-changing work
Completion criteria
Required evidence
True User decision boundary
Result/report contract
```

Prefer outcome-oriented constraints over a detailed itinerary.

## Durable coordinates

A FORMAL task records the repository/task coordinates needed to recover the authorized work, including branch/baseline when applicable and the pinned collaboration revision.

Execution begins from the authorized current task state and finishes with the intended final state and report published remotely. `execution.md` owns repository-state safety, tmp/worktree placement, branch hygiene, and concurrency safety.

## Follow-through

Within scope, Codex persists through implementation, execution, failures caused by the change, bounded repair, and reruns until completion criteria are met.

Stop only for a concrete blocker or true decision boundary. A discovered `DESIGN_GAP` stops the affected semantic path rather than inventing missing Design.

## FORMAL report

Codex writes the bound report after execution. It records:

```text
what changed
what evidence actually ran
material deviations/limitations
final repository coordinates
design_signal: none | design_change | design_drift | design_gap
unresolved blocker if any
```

The report is append-only historical evidence. It does not redefine current Design and its verdict is not final acceptance.

## Acceptance and Design synchronization

Codex supplies evidence; ChatGPT issues:

```text
PASS | PASS WITH LIMITATIONS | BLOCKED | FAIL
```

Acceptance asks whether the intended outcome is satisfied, evidence is sufficient, and any material boundary was crossed.

After acceptance, ChatGPT must classify the Design consequence:

```text
accepted Design change
→ update the owning current Design topic in the same work unit

execution/evidence only
→ no Design change

design_gap / unresolved scientific-product meaning
→ surface the exact decision; do not guess
```

Do not wait for periodic reconciliation when the accepted consequence is already known. `project/reconciliation.md` is the backstop for missed/accumulated deltas.

A material acceptance/adjudication may itself be preserved as a `reports/chatgpt/` acceptance record when future reconstruction benefits.

## Integration

A FORMAL task declares:

```text
Post-acceptance integration: AUTO | USER_CHECKPOINT
```

Use `USER_CHECKPOINT` only when integration itself is a genuine User decision such as release/publication authorization, destructive migration, unresolved scientific/product choice, visibility/licensing change, or another explicit checkpoint.

Task execution may be parallel, but integration into the accepted branch/state is serialized. After one task integrates, every later task re-establishes compatibility with the newly current remote state before its own integration.

After successful integration and publication:

```text
remove task linked worktree when no recovery value remains
→ delete the local/remote task branch when no longer needed
→ prune stale worktree registrations when appropriate
```

Do not retain completed task branches as historical archives; Git history and append-only ChatGPT/Codex records preserve the task history. Do not delete a blocked/dirty/unpublished branch or worktree merely to satisfy branch-count targets.

## Completion shorthand

When the User says `Codex 已完成`, ChatGPT resolves the relevant task/report, performs acceptance, synchronizes current Design when applicable, and then proceeds with permitted serialized integration and task-state cleanup.

Do not create a separate completion registry.

## User-visible task link

After the task is committed, use the exact minimal Codex task-link format owned by `execution.md`:

```text
任务链接：
<IMMUTABLE_GITHUB_TASK_URL>
```

Do not duplicate task coordinates or task-body prose in chat.
