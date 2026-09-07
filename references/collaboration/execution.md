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

Repository-only work remains DIRECT when connected ChatGPT capability can perform and verify the required changes itself. Do not delegate to Codex merely because a change spans many repository files, uses a task branch, or benefits from an auditable commit. Typical DIRECT examples include GitHub-side file moves/renames, report or metadata normalization, connected repository cleanup, Markdown/reference repair, and other deterministic repository mutations that require no User-machine filesystem, runtime, environment, browser, external CLI, or local execution evidence.

Codex is justified only by a genuinely local requirement or evidence dependency. A pre-existing FORMAL task does not by itself convert otherwise connected/DIRECT work into LOCAL work; when execution ownership was misclassified, durably amend/supersede the task if needed and let ChatGPT complete the repository-connected portion directly.

If local evidence remains, DIRECT authoring may feed LOCAL-QUICK or FORMAL rather than transferring the whole deliverable.

### LOCAL-QUICK

Use for small, low-risk, reviewable local implementation, verification, or bounded repair when there is no unresolved scientific/product/design decision, destructive/shared-state migration, material security/credential change, public/trust contract, or need for a durable task/report audit chain.

```text
concise Codex instruction
→ verify activated shared Skills
→ establish project-local temporary workspace if needed
→ implement/verify/repair
→ focused evidence
→ clean temporary state with no recovery value
→ task-scoped commit/push when repository state changed
→ concise result
→ ChatGPT acceptance review
```

Escalate if execution exposes design ambiguity, material risk, or scope growth.

### FORMAL

Use for major architecture/cross-module work, scientific/product/trust/public-contract migration, persistent/destructive shared state, long multi-step local work, high security/data-loss/reproducibility risk, release qualification, or work needing durable audit evidence.

FORMAL uses a committed task/report lifecycle owned by `formal.md`. Route directly to that owner from `SKILL.md` when FORMAL semantics are needed.

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

All Agent-created persistent local scratch state on the User machine belongs under the target project's root:

```text
<PROJECT_ROOT>/tmp/<WORK_ID>/
```

`WORK_ID` is:

```text
FORMAL      → exact task_id
LOCAL-QUICK → short local work/session label unique enough within the project
```

This boundary covers Agent-chosen linked worktrees, scratch repositories, temporary downloads, test/E2E outputs, render outputs, caches, intermediates, and disposable environments.

Agents MUST NOT create persistent sibling project worktrees, Desktop test folders, Documents-root scratch directories, or ad-hoc persistent `/tmp/<project>-...` workspaces merely for convenience unless the User explicitly authorizes that exact location.

Typical task-local layout is created only as needed:

```text
<PROJECT_ROOT>/tmp/<WORK_ID>/
├── worktree/
├── run/
├── downloads/
├── cache/
├── renders/
└── env/
```

Do not create unused ceremonial subdirectories.

System/runtime caches whose path is controlled by the OS or an external tool and cannot reasonably be redirected are outside this Agent-chosen boundary; do not deliberately select them as project scratch space.

A maintained repository should normally ignore its root `tmp/` path. Task scratch state is not committed.

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

At the start of a new local task, Codex may inspect only the active project's `tmp/` for clearly stale completed Agent state. Do not scan unrelated projects merely as ceremony. A User-explicit housekeeping task may authorize broader cleanup.

## Linked worktrees

For FORMAL work that needs a linked worktree, default to:

```text
<PROJECT_ROOT>/tmp/<TASK_ID>/worktree/
```

Registered worktrees are removed through Git-aware operations such as `git worktree remove`, followed by `git worktree prune` when appropriate. Do not blindly `rm -rf` a registered worktree.

If the primary checkout cannot safely host the default path because of a real Git/worktree limitation, use the nearest project-owned `tmp/` boundary that preserves one canonical project root and report the exception. Do not default to a sibling directory.

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

A merge/rebase/cherry-pick that changes task ancestry is an explicit reconciliation decision, not implicit execution permission.

## Ownership boundary

If the in-scope owner is correct while an out-of-scope downstream consumer remains stale:

```text
make current owner conform
→ verify it
→ report downstream drift
→ stop at ownership boundary
```

Do not restore rejected upstream interfaces merely to make unrelated downstream tests green.

Component/stage acceptance is not the same as default-branch/full-system acceptance.

## Concurrency

Independent work may run concurrently only when branches/worktrees and other mutable resources do not interfere.

A FORMAL task branch has one active execution owner. The default branch is not frozen merely because an isolated task branch exists. If non-interference cannot be established, serialize the work.
