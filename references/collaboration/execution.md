# Execution and local-state contract

Load this reference for DIRECT/LOCAL-QUICK/FORMAL route selection, Codex-local execution, repository publication safety, temporary state, or concurrency.

## Choose the lightest route

### DIRECT
Use when ChatGPT can complete the work and obtain the required evidence with connected capabilities.

Material DIRECT repository/design work may be preserved as a concise `reports/chatgpt/` direct record when future reconstruction would benefit.

### LOCAL-QUICK
Use for bounded local implementation/verification/filesystem work with no unresolved scientific/product decision, destructive/shared-state migration, security/credential change, public/release action, or other material trust boundary.

LOCAL-QUICK uses:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md  task specification
reports/codex/YYMMDD_codex_NN.md      concise execution record
```

The Codex record is intentionally short but durable.

### FORMAL
Use when the work is materially higher-risk or benefits from a richer durable execution record: major architecture/cross-module changes, scientific/product/trust contract work, persistent/destructive shared state, long multi-step local work, release qualification, or comparable security/reproducibility risk.

FORMAL lifecycle is owned by `formal.md`.

## Task specification

Every Codex repository task is committed under `reports/chatgpt/` before execution.

The task states intended outcome, authority/boundaries, scope, completion criteria, required evidence, and true decision boundary. Chat carries only the locator.

Avoid command-by-command instructions unless a specific sequence is itself required for correctness, reproducibility, or safety.

## Execution autonomy

Within authorized scope, Codex may choose the engineering path:

```text
inspect → implement → run → diagnose → repair → rerun
```

Continue until completion criteria are met or a real blocker/decision boundary is reached.

## Repository-state safety

For repository-changing local work, two properties are required.

Before mutation:

```text
execution is based on the authorized current remote/task state
AND pre-existing User work is understood and preserved
```

At completion:

```text
the intended task-scoped changes and Codex record are committed/published
AND the final local result corresponds to the final remote task/work state
```

Codex chooses appropriate Git/branch/worktree operations to establish those properties. Do not use destructive reset, force push, hidden stash, or unrelated conflict rewriting merely to manufacture alignment.

If the authorized baseline or final published state cannot be established without risking User work or choosing among conflicting histories, stop with the concrete blocker.

## Durable Codex record

Every Codex task writes one append-only `reports/codex/YYMMDD_codex_NN.md` record.

LOCAL-QUICK records only the essential facts:

```text
task_id / task source
what changed
final repository coordinates
focused evidence
limitations/blocker if any
design_signal: none | design_change | design_drift | design_gap
```

FORMAL uses the richer report contract from `formal.md`.

A Codex record reports evidence; it does not redefine Design or self-accept.

## Design signal

When execution exposes a current-design consequence, record it explicitly rather than burying it in prose:

```text
design_change  accepted task/result appears to change current Design
design_drift   implementation/current owner no longer matches accepted Design
design_gap     current Design does not determine required semantics
none           no Design consequence
```

ChatGPT acceptance handles current Design under `project/reconciliation.md` and `project/design.md`.

## Local scratch

Task-created persistent scratch on the User machine belongs under `<PROJECT_ROOT>/tmp/<WORK_ID>/`.

Use only what the task needs. Remove disposable state when complete; retain blocked-state material only when it has clear recovery value.

A linked worktree is optional. Use one when isolation materially reduces interference.

## Verification and repair

Run checks appropriate to the change and required claim. If they pass, do not broaden or repeat testing unless new changes, failures, risk, or unresolved concerns justify it.

Failures caused by the in-scope change should normally be diagnosed and repaired within scope rather than escalated as approval questions.

## Ownership boundary

If the current owner is correct and an out-of-scope consumer is stale, report downstream drift rather than weakening the current contract to make unrelated checks pass.

## Concurrency

Parallel work is allowed when mutable resources do not interfere. If non-interference is unclear, serialize rather than adding coordination machinery by default.
