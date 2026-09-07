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
→ verify activated shared Skills when applicable
→ establish project-local temporary workspace if needed
→ implement/verify/repair
→ focused evidence
→ clean temporary state with no recovery value
→ task-scoped commit/push when required
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

## Git safety

For repository-changing LOCAL work:

```text
fetch
→ inspect branch / HEAD / upstream / worktree
→ preserve pre-existing User state
→ reach the authorized task/work branch safely
→ commit only task-scoped changes
→ push the owning branch
→ fetch/verify pushed state when practical
```

Do not infer permission for destructive reset, force-push, hidden automatic stash, or non-trivial conflict reconciliation.

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
