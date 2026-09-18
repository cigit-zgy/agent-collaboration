# Execution and local-state contract

Load this reference for DIRECT/LOCAL-QUICK/FORMAL route selection, Codex-local execution, repository publication safety, temporary state, branches/worktrees, or concurrency.

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

For repository-changing work, the task also declares the mutation surface needed for concurrency safety. Prefer repository-relative paths and semantic owners rather than exhaustive file inventories.

```yaml
mutation_scope:
  - <repository-relative path or semantic owner>
concurrency_keys:
  - <shared owner/resource key when applicable>
```

Avoid command-by-command instructions unless a specific sequence is itself required for correctness, reproducibility, or safety.

## User-visible repository-change summary

Whenever ChatGPT changes GitHub repository content, the user-visible response includes a compact change summary, ordered by importance and limited to the ten most important changed artifacts:

```text
本次更改内容：

1. <名称>: <GitHub link>
2. <名称>: <GitHub link>
```

Rules:

- include only artifacts actually changed/published in the current work unit;
- order by user/project importance, not commit chronology;
- show at most 10 items;
- use a direct GitHub link to the changed file, task, report, commit, or other most useful durable artifact;
- do not add a second long prose recap of the same changes unless the User asks.

When ChatGPT issues a Codex task, the user-visible console handoff is always one copyable fenced code block. Target 5–7 lines; hard maximum 10 lines.

Use this canonical 6-line shape:

```text
任务: <ONE SHORT MISSION LINE>
范围: <ONE SHORT SCOPE LINE>
完成: <ONE SHORT COMPLETION/EVIDENCE LINE>
任务链接：
<IMMUTABLE_GITHUB_TASK_URL>
以链接内 committed task 为唯一执行规范。
```

The three summary lines are navigation only, not task authority. They may summarize only mission, bounded scope, and completion/evidence at a high level. They MUST NOT restate command sequences, file inventories, prohibitions, verification matrices, dependency details, branch mechanics, or the task body.

The immutable URL points to the committed `reports/chatgpt/...` task at its task-containing commit. The committed task is the sole task-specific authority. Do not attach, generate, export, materialize, or offer a downloadable `.md` copy of the task. The GitHub link is the task handoff. Do not add prose before or after the fenced block unless the User explicitly asks.

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

Codex chooses appropriate Git operations to establish those properties. Do not use destructive reset, force push, hidden stash, or unrelated conflict rewriting merely to manufacture alignment.

If the authorized baseline or final published state cannot be established without risking User work or choosing among conflicting histories, stop with the concrete blocker.

## Task branches and linked worktrees

Repository-changing Codex work uses the smallest branch/worktree footprint that safely isolates the task.

```text
read-only/local-only task
→ no task branch/worktree unless genuinely needed

repository-changing task
→ at most one task branch
→ normally one linked worktree at <PROJECT_ROOT>/tmp/<WORK_ID>/worktree/
→ all bounded repair stays on that same branch/worktree
```

Do not create nested repair branches, experiment branches, or additional worktrees merely because a task encounters ordinary implementation failures. A superseding task may create a new branch only when task semantics materially change.

The linked worktree is a real Git checkout even though it lives under `tmp/`. Source, tests, Design, Skill Markdown, reports, and other repository artifacts are edited at their normal repository-relative paths inside that worktree.

A completed project artifact must never exist only as an uncommitted file under `tmp/`. Before completion, retained `.py`, `.md`, `.yaml`, config, tests, Design, Skill, or report changes must be committed/published on the task branch or otherwise placed in their real durable owner.

## Local scratch

All task-local temporary state remains under:

```text
<PROJECT_ROOT>/tmp/<WORK_ID>/
```

Typical layout:

```text
worktree/   linked Git checkout for the active task when needed
run/        transient runtime output
cache/      disposable cache
renders/    disposable render output
downloads/  temporary downloads
```

`tmp/` is not an alternative project tree or durable result owner. The worktree may contain real project files because it is a Git checkout; disposable outputs outside the worktree must not be promoted accidentally.

Do not remove an active/dirty/unpublished worktree as generic tmp cleanup. After the task is safely published and no recovery value remains, remove the linked worktree with Git-aware cleanup (`git worktree remove` / `git worktree prune` as appropriate) and remove disposable task scratch.

## Parallel-task safety

Multiple Codex windows may operate on one repository only when their mutation surfaces do not conflict.

Before starting mutation, inspect currently active linked worktrees/task branches and the durable task specifications when needed. Parallel execution is allowed only when both are true:

```text
mutation_scope does not overlap materially
AND concurrency_keys do not overlap
```

Treat the same semantic owner as overlapping even when two tasks currently touch different files.

Shared authority surfaces serialize by default, including repository constitution/current-state/living-Design and other project-declared shared schema/config/public-interface owners. Examples include:

```text
AGENTS.md
CURRENT.md
reports/design/**
shared workflow/Skill semantics
central schemas or public interfaces declared as shared owners
```

If non-interference cannot be established cheaply, serialize instead of adding coordination machinery.

### Active-concurrency cap

Per repository, keep repository-changing Codex tasks deliberately small in number:

```text
normal target: <= 4 active task worktrees/branches
5th concurrent repo-changing task: serialize unless the User explicitly overrides
```

Read-only tasks do not count toward this cap.

## Branch hygiene

Temporary task branches are execution state, not history storage.

```text
normal target: <= 10 temporary remote task branches
>= 15 temporary remote task branches:
  perform branch hygiene before opening another routine task branch
after cleanup target: <= 8
```

Cleanup rules:

```text
accepted + integrated
→ remove linked worktree
→ delete local/remote task branch when no longer needed

cancelled / superseded / rejected
→ do not merge merely to reduce branch count
→ first preserve any uniquely valuable state in its real durable owner
→ then delete branch/worktree

blocked + deliberate recovery value
→ retain only while recovery is genuinely expected

unknown / dirty / unpublished
→ inspect before deletion

age alone
→ never sufficient reason to delete
```

Do not merge a branch solely for branch-count hygiene.

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

## Verification and repair

Run checks appropriate to the change and required claim. If they pass, do not broaden or repeat testing unless new changes, failures, risk, or unresolved concerns justify it.

Failures caused by the in-scope change should normally be diagnosed and repaired within scope rather than escalated as approval questions.

## Integration discipline

Parallel task execution may be concurrent; integration into the current accepted branch/state is serialized.

After each accepted integration, later task branches refresh against the newly current remote state and re-establish that their result remains valid before their own integration.

Do not allow several task agents to mutate the canonical accepted branch concurrently.

## Ownership boundary

If the current owner is correct and an out-of-scope consumer is stale, report downstream drift rather than weakening the current contract to make unrelated checks pass.
