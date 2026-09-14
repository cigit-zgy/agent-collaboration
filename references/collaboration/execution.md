# Execution and local-state contract

Load this reference for DIRECT/LOCAL-QUICK/FORMAL route selection, Codex-local execution, repository publication safety, temporary state, or concurrency.

## Choose the lightest route

### DIRECT
Use when ChatGPT can complete the work and obtain the required evidence with connected capabilities.

### LOCAL-QUICK
Use for bounded local implementation/verification/filesystem work with no unresolved scientific/product decision, destructive/shared-state migration, security/credential change, public/release action, or other material trust boundary.

LOCAL-QUICK still uses a committed `reports/chatgpt/` task but no `reports/codex/` report.

### FORMAL
Use when the work is materially higher-risk or benefits from durable execution evidence: major architecture/cross-module changes, scientific/product/trust contract work, persistent/destructive shared state, long multi-step local work, release qualification, or comparable security/reproducibility risk.

FORMAL lifecycle is owned by `formal.md`.

## Task specification

Every Codex repository task is committed under:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

The task states the intended outcome, authority/boundaries, scope, completion criteria, required evidence, and true decision boundary. Chat carries only the locator.

Avoid command-by-command instructions unless a specific command sequence is itself required for correctness, reproducibility, or safety.

## Execution autonomy

Within the authorized scope, Codex may choose the engineering path:

```text
inspect → implement → run → diagnose → repair → rerun
```

It should continue until the task's completion criteria are met or a real decision boundary/blocker is reached.

Do not stop merely to ask permission for routine reversible implementation choices.

## Repository-state safety

For repository-changing local work, two properties are required.

Before mutation:

```text
execution is based on the authorized current remote/task state
AND pre-existing User work is understood and preserved
```

At completion:

```text
the intended task-scoped changes are committed/published as required
AND the final local result corresponds to the final remote task/work state
```

Codex chooses the appropriate Git/branch/worktree operations to establish those properties. Do not use destructive reset, force push, hidden stash, or unrelated conflict rewriting merely to manufacture alignment.

If the authorized baseline or final published state cannot be established without risking User work or choosing among conflicting histories, stop with the concrete blocker.

## Local scratch

Task-created persistent scratch on the User machine belongs under:

```text
<PROJECT_ROOT>/tmp/<WORK_ID>/
```

Use only what the task needs. Remove disposable state when the work is complete; retain blocked-state material only when it has clear recovery value.

A linked worktree is optional, not mandatory. Use one when isolation materially reduces interference; otherwise prefer the simpler safe arrangement.

## Verification and repair

Run checks appropriate to the change and required claim. If they pass, do not broaden or repeat testing unless new changes, failures, risk, or unresolved concerns justify it.

Failures caused by the in-scope change should normally be diagnosed and repaired within scope rather than escalated as approval questions.

## Ownership boundary

If the current owner is correct and an out-of-scope consumer is stale, report the downstream drift rather than weakening the current contract to make unrelated checks pass.

## Concurrency

Parallel work is allowed when mutable resources do not interfere. If non-interference is unclear, serialize rather than adding coordination machinery by default.
