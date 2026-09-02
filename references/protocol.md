# Collaboration protocol

## Roles

### User

- defines the goal;
- makes scientific and product decisions;
- resolves genuine human-only ambiguity;
- approves exceptional scope changes.

### ChatGPT

ChatGPT is the planner, formal task author, independent auditor, and acceptance
authority. Before writing a task, it inspects the target repository and current
evidence. It writes formal tasks under `reports/chatgpt/`, commits and pushes the
task, then gives the User only the short Codex launch prompt.

After Codex finishes, ChatGPT independently checks the repository, diff,
implementation, Codex report, verification evidence, and relevant artifacts. It
does not accept Codex's self-reported PASS. ChatGPT decides `PASS`,
`PASS WITH LIMITATIONS`, `BLOCKED`, or `FAIL`, and only then decides whether to
open the next task.

When a discussion produces a durable project decision, ChatGPT updates the
appropriate topic under `reports/concept/`. Concept files capture current design
truth, not task execution history.

### Codex

Codex is the implementer. It executes the committed formal task rather than
guessing requirements from chat. It does not expand scope without approval. It
implements, runs the specified verification, writes its implementation report under
`reports/codex/`, commits, and pushes. Codex does not grant final acceptance and
does not rewrite project concepts unless the committed task explicitly requires it.

## Standard loop

```text
User requirement
→ ChatGPT independent inspection
→ durable concept update when needed
→ ChatGPT formal committed task in reports/chatgpt/
→ short Codex launch prompt
→ Codex repository synchronization
→ Codex implementation
→ Codex verification
→ Codex report in reports/codex/ + commit/push
→ Codex final synchronization check
→ ChatGPT independent audit
→ verdict
→ concept update when acceptance changes durable project truth
→ only then next task
```

## Repository synchronization

For a formal task, local state and the tracked remote branch must be explicit at
both ends of the task.

Before implementation Codex must:

1. run `git fetch` for the task repository;
2. inspect the current branch, `HEAD`, configured upstream, and `git status --short`;
3. preserve pre-existing user changes; never discard, overwrite, or hide them;
4. when the worktree is safe and the current branch is only behind its upstream,
   fast-forward to the fetched upstream state;
5. stop and report the conflict instead of inventing a merge/rebase when the branch
   has diverged or existing user changes make synchronization unsafe;
6. verify that the committed task source and stated baseline are consistent with
   the synchronized repository before editing.

A formal task does not authorize `reset --hard`, force-push, destructive cleanup,
or an implicit merge/rebase. Automatic stashing is not a substitute for preserving
user work.

After implementation Codex must:

1. commit all task-scoped repository changes required by the task;
2. push the current branch to its configured upstream;
3. fetch again;
4. verify `HEAD` equals the fetched upstream branch tip;
5. report the final worktree state and any intentionally preserved pre-existing
   changes.

`HEAD == upstream` is the normal completion condition for repository changes. If it
cannot be achieved safely, the task report must state why and must not claim a clean
Git synchronization PASS.

## Report ownership

```text
reports/chatgpt/
→ committed ChatGPT task specifications

reports/codex/
→ Codex implementation and verification reports

reports/concept/
→ durable User + ChatGPT project decisions and design contracts
```

Do not use these directories interchangeably. Do not place transient run logs in
`reports/concept/`. Existing legacy report directories do not need retrospective
renaming unless a project task explicitly requests migration.

## Invariants

- One formal task is active at a time.
- The next formal task starts only after independent audit of the previous task.
- Codex implements; ChatGPT accepts.
- Evidence, not self-reported PASS, determines completion.
- Scientific and product rigor is mandatory; engineering ceremony is not.
