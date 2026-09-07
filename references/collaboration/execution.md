# Execution and local-state contract

Load this reference for DIRECT/LOCAL-QUICK/FORMAL route selection, Codex-local execution, Git/worktree safety, temporary-state placement, or concurrency.

## Route selection

Use the lightest route that preserves the required trust and evidence.

### DIRECT

Use when ChatGPT can complete the work with connected capability and all required evidence is available without substantial local setup.

```text
ChatGPT authors/executes
→ runs supported cheap verification
→ completes
```

Repository-only work remains DIRECT when connected ChatGPT capability can perform and verify the required changes itself. Do not delegate to Codex merely because a change spans many repository files, uses a task branch, or benefits from an auditable commit.

Codex is justified only by a genuinely local requirement or evidence dependency. If local evidence remains, DIRECT authoring may feed LOCAL-QUICK or FORMAL rather than transferring the whole deliverable.

## Durable Codex-task specification — hard boundary

Every repository task delegated to Codex, whether `LOCAL-QUICK` or `FORMAL`, MUST first be written, committed, and pushed as:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

The committed task artifact is the sole task-specific execution specification.

Chat MUST NOT carry the detailed task body. Do not paste or paraphrase command sequences, path inventories, prohibitions, acceptance criteria, verification matrices, branch rules, or long safety instructions into the User-visible Codex prompt.

User-visible delegation contains only a very short locator to the committed task. Exact LOCAL-QUICK and FORMAL locator formats live in their templates.

If ChatGPT cannot commit/push the task artifact, do not substitute a long chat-only prompt; report the repository-write blocker.

### LOCAL-QUICK

Use for bounded, low-risk, reviewable local implementation, verification, filesystem work, or repair when there is no unresolved scientific/product/design decision, material destructive/shared-state migration, security/credential change, public/trust contract, release qualification, or other FORMAL trigger.

LOCAL-QUICK still uses a durable `reports/chatgpt/` task artifact, but it does **not** create a `reports/codex/` report.

```text
committed LOCAL-QUICK task
→ short copyable locator
→ pre-execution remote synchronization handshake
→ verify activated shared Skills when applicable
→ establish project-local temporary workspace if needed
→ implement/verify/repair
→ focused evidence
→ clean temporary state with no recovery value
→ task-scoped commit/push when required
→ post-execution remote synchronization handshake
→ return only the task's compact Result contract
→ ChatGPT acceptance review when needed
```

The LOCAL-QUICK task template is:

```text
templates/local-quick-task.md
```

If execution exposes unresolved design, material scope/risk growth, destructive/shared-state behavior, release/public-contract work, or another FORMAL boundary:

```text
STOP affected execution
→ return BLOCKED with the escalation reason
→ do not extend the task through chat instructions
→ ChatGPT issues a new FORMAL task if continuation is approved
```

### FORMAL

Use for major architecture/cross-module work, scientific/product/trust/public-contract migration, persistent/destructive shared state, long multi-step local work, high security/data-loss/reproducibility risk, release qualification, or work needing durable execution evidence.

FORMAL uses both:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
reports/codex/YYMMDD_codex_NN.md
```

FORMAL lifecycle is owned by `formal.md`.

## Authoring versus execution

Do not classify a whole code deliverable as LOCAL merely because final verification requires the User machine.

```text
ChatGPT-authorable design/code/tests
→ ChatGPT writes first

cheap connected verification
→ ChatGPT runs before handoff

project/runtime/local-feedback work
→ Codex executes locally and performs bounded repair
```

Detailed implementation quality belongs to `implementation.md`; verification levels/evidence belong to `verification.md`.

## Local ephemeral state — hard boundary

All Agent-created persistent local scratch state on the User machine belongs under:

```text
<PROJECT_ROOT>/tmp/<WORK_ID>/
```

`WORK_ID` is the task's durable `task_id` when one exists; otherwise use a short project-local work label. This boundary covers linked worktrees, scratch repositories, temporary downloads, test/E2E outputs, renders, caches, intermediates, and disposable environments.

Agents MUST NOT create persistent sibling project worktrees, Desktop test folders, Documents-root scratch directories, or ad-hoc persistent `/tmp/<project>-...` workspaces merely for convenience unless the User explicitly authorizes that exact location.

Create only needed subdirectories, for example:

```text
worktree/
run/
downloads/
cache/
renders/
env/
```

Task scratch state is not committed.

## Cleanup lifecycle

```text
completed + no recovery value
→ remove work tmp immediately

BLOCKED/FAIL + deliberate recovery value
→ retain only the minimum needed state and report why

superseded/cancelled + no recovery value
→ remove work tmp

active/dirty/unpushed/uncertain
→ preserve until safety is established
```

Age alone never authorizes deletion.

## Linked worktrees

When a delegated task needs a linked worktree, prefer:

```text
<PROJECT_ROOT>/tmp/<TASK_ID>/worktree/
```

Registered worktrees are removed through Git-aware operations such as `git worktree remove`, followed by `git worktree prune` when appropriate. Do not blindly `rm -rf` a registered worktree.

## Remote synchronization handshake — hard boundary

Every **repository-changing** Codex task, whether `LOCAL-QUICK` or `FORMAL`, MUST prove that Codex starts from the same authorized remote state that ChatGPT/task authority published and ends with the same task state visible remotely.

### Before any repository mutation

Codex MUST:

```text
fresh-fetch the authorized remote refs
→ inspect repository identity / branch / HEAD / upstream / worktrees / pre-existing User changes
→ resolve the exact authorized task/baseline coordinate from the committed task + remote branch
→ establish the task checkout/worktree safely
→ prove local execution HEAD == authorized fetched remote baseline
→ only then mutate repository state
```

The fetched remote state, not a stale local checkout, is the synchronization reference.

For a pinned task branch, an unexpected remote branch head or a mismatch between the committed task coordinate and fetched remote state is a synchronization conflict. Do not silently adopt a different baseline or keep working from the stale local copy. Stop and report the conflict unless the committed task explicitly defines the reconciliation.

This rule does **not** require blind `git pull` on the primary checkout. Prefer `git fetch` plus a safe branch/worktree arrangement. Do not use reset, rebase, stash, force checkout, force push, or destructive reconciliation merely to make local state match remote.

### After repository changes

Before reporting repository-changing task completion, Codex MUST:

```text
commit task-scoped changes
→ push the owning task/work branch
→ fresh-fetch the remote again after push
→ resolve fetched upstream task/work branch HEAD
→ prove local task HEAD == fetched upstream HEAD
→ confirm any required task worktree cleanliness
→ only then report PASS/completion
```

A successful `git push` exit status alone is insufficient evidence. Post-push equality is mandatory, not `when practical`.

If the post-push fresh fetch shows:

```text
local task HEAD != fetched upstream task/work branch HEAD
```

then Codex MUST NOT report PASS. Preserve local/User state and return `BLOCKED` or `FAIL` according to the concrete cause.

A read-only/local-only Codex task that intentionally makes no repository change does not need a push step, but it still resolves current remote/project authority when repository state materially affects the result.

## Git safety

For repository-changing LOCAL work, the synchronization handshake and task-scoped Git rules combine as:

```text
fresh fetch
→ inspect branch / HEAD / upstream / worktrees / User state
→ prove exact authorized remote baseline locally
→ preserve pre-existing User state
→ perform task work
→ commit only task-scoped changes
→ push owning branch
→ fresh fetch again
→ prove local HEAD == upstream HEAD
```

Do not infer permission for destructive reset, force-push, hidden automatic stash, non-trivial conflict reconciliation, or direct mutation of a stale primary checkout.

## Ownership boundary

If the in-scope owner is correct while an out-of-scope downstream consumer remains stale:

```text
make current owner conform
→ verify it
→ report downstream drift
→ stop at ownership boundary
```

Do not restore rejected upstream interfaces merely to make unrelated downstream tests green.

## Concurrency

Independent work may run concurrently only when branches/worktrees and other mutable resources do not interfere. A delegated task branch has one active execution owner. If non-interference cannot be established, serialize the work.
