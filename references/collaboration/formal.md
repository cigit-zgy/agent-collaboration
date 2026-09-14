# FORMAL task, report, acceptance, and integration contract

Load this reference for FORMAL delegation, task/report binding, acceptance review, or post-acceptance integration.

FORMAL uses:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
reports/codex/YYMMDD_codex_NN.md
```

Exact artifact templates are cold and loaded only when creating/reviewing those files.

## When FORMAL is appropriate

Use FORMAL when the work has material architectural, scientific/product, trust, destructive/shared-state, security, release, reproducibility, or long-running execution risk that benefits from a durable execution record.

Do not choose FORMAL merely because a task is large in line count.

## Task authority

The committed `reports/chatgpt/` task is the sole task-specific execution specification. Chat is only a locator.

A good task defines:

```text
Mission / intended outcome
Authority and frozen boundaries
Scope / material non-goals
Completion criteria
Required evidence
True User decision boundary
Result/report contract
```

Prefer outcome-oriented constraints over a detailed itinerary. Codex may choose the implementation path inside the authorized scope.

## Durable coordinates

A FORMAL task records the repository/task coordinates needed to recover the authorized work, including the task branch/baseline when applicable and the pinned collaboration revision.

The execution must begin from the authorized current task state and finish with the intended final state published remotely. `execution.md` owns those safety properties; the task need not restate Git choreography.

## Follow-through

Within scope, Codex should persist through implementation, execution, failures caused by the change, bounded repair, and reruns until the completion criteria are met.

Stop only for a concrete blocker or a true decision boundary defined by `protocol.md` or the task.

A discovered `DESIGN_GAP` stops only the affected semantic path; Codex does not invent the missing design to finish the task.

## FORMAL report

Codex writes the bound report after execution. The report records what changed, what evidence actually ran, material deviations/limitations, final repository coordinates, and any unresolved blocker. It does not restate the full task or redefine Design.

## Acceptance

Codex supplies evidence; ChatGPT issues:

```text
PASS | PASS WITH LIMITATIONS | BLOCKED | FAIL
```

Acceptance asks whether the task's stated outcome and completion criteria are satisfied, whether the evidence is sufficient for the claim, and whether any material boundary was crossed.

Do not require an additional reviewer merely for ceremony. Add one only when the scientific, architectural, trust, security, or release risk benefits from an independent perspective.

## Integration

A FORMAL task declares:

```text
Post-acceptance integration: AUTO | USER_CHECKPOINT
```

Use `USER_CHECKPOINT` only when integration itself is a genuine User decision, such as release/publication authorization, destructive migration, unresolved scientific/product choice, visibility/licensing change, or another explicit checkpoint.

## Completion shorthand

When the User says `Codex 已完成`, ChatGPT resolves the relevant task/report and performs acceptance review. Do not create a separate completion registry.

## User-visible locator

After the task is committed, the User receives only the short immutable locator defined by the task template. Do not duplicate the task body in chat.
