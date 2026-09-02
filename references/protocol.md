# Collaboration protocol

## Shared authority and entrypoints

`agent-collaboration` is the shared operating source for the three-party workflow:

```text
User ↔ ChatGPT ↔ Codex
```

The three roles use the same protocol but enter it differently:

- Codex is routed here automatically by the machine-wide `~/.codex/AGENTS.md` for
  formal ChatGPT ↔ Codex repository work.
- ChatGPT is not assumed to discover the User's local Skill automatically in a new
  conversation. The User explicitly asks ChatGPT to use `agent-collaboration` and
  identifies the target project repository.
- Each project's root `AGENTS.md` is its project-level entry point and constitution.
  It links back to the canonical collaboration repository and routes project-owned
  Skills, concepts, and reports.
- The User remains the final human authority for goals, scientific/product choices,
  and genuine human-only ambiguity.

No participant should maintain a competing copy of this workflow in project notes or
chat prompts. Project `AGENTS.md` files add project-specific rules but route global
collaboration back to this Skill rather than duplicating it.

## Roles

### User

- defines the goal;
- makes scientific and product decisions;
- resolves genuine human-only ambiguity;
- approves exceptional scope changes;
- explicitly invokes this collaboration protocol for ChatGPT in a new conversation
  when it is needed.

### ChatGPT

ChatGPT is the planner, design partner, remote-capable executor, formal task author,
independent auditor, and acceptance authority.

User + ChatGPT own design. Before delegation, ChatGPT must inspect the target
repository and current evidence, resolve every design decision that can reasonably be
resolved through User interaction and available sources, record durable conclusions
in the project concept assets when appropriate, and decide whether Codex is actually
required.

### Delegation boundary

ChatGPT must not delegate work merely because Codex is capable of doing it.

If ChatGPT can safely and completely perform a task using its currently available
connected tools, it should do that work directly and verify the result itself. Typical
examples include repository inspection, design clarification, concept/report updates,
formal task authoring, and deterministic repository text changes supported by the
connected repository tooling.

Codex should receive only work that materially requires a local-machine capability
unavailable to ChatGPT, such as:

- local filesystem or uncommitted worktree state;
- local CLI/tool installation or invocation;
- project runtime/environment execution;
- local tests, builds, rendering, or large artifacts;
- credentials/secrets or machine-local services;
- local Git operations that cannot be safely completed through ChatGPT's connected
  repository tools;
- another explicit capability unavailable to ChatGPT.

When Codex is required, ChatGPT must remove avoidable design discretion before
handoff. The committed task should freeze every decision that can reasonably be
frozen: exact scope, authoritative sources, affected files/areas, required behavior,
non-goals, engineering constraints, verification level, acceptance criteria, Git
requirements, report path, and fixed stdout. Include exact commands or replacement
text when they materially reduce ambiguity.

Codex executes; it does not redesign. If the committed task contains a contradiction,
a missing prerequisite, an infeasible instruction, or a design-affecting ambiguity,
Codex reports it instead of silently choosing a new architecture, scientific/product
meaning, or scope. Codex may choose incidental coding mechanics only when those
choices do not change approved behavior, architecture, scientific/product semantics,
or task boundaries.

For a Codex task, ChatGPT writes the formal specification under the target project's
`reports/chatgpt/`, commits and pushes it, then gives the User only the short Codex
launch prompt.

After Codex finishes, ChatGPT independently checks the target repository, diff,
implementation, Codex report, verification evidence, and relevant artifacts. It does
not accept Codex's self-reported PASS. ChatGPT decides `PASS`,
`PASS WITH LIMITATIONS`, `BLOCKED`, or `FAIL`, and only then decides whether to open
the next task.

When a discussion produces a durable project decision, ChatGPT updates the
appropriate topic under the target project's `reports/concept/`. Concept files
capture current design truth and its decision history, not task execution history.

### Codex

Codex is the local implementer/executor for committed tasks that require local
capabilities. It executes the committed formal task rather than guessing requirements
from chat. It does not expand scope or make design decisions without approval. It
implements, runs the specified verification, writes its implementation report under
the target project's `reports/codex/`, commits, and pushes. Codex does not grant final
acceptance and does not rewrite project concepts unless the committed task explicitly
requires a mechanical concept update already designed by User + ChatGPT.

## Project integration

`agent-collaboration` owns the collaboration protocol. Each project owns its own work
records.

```text
agent-collaboration
= how the three roles collaborate

project/AGENTS.md
= project constitution and project-level entry/router

project/SKILL.md
= project workflow/router

project/reports/concept/
= durable User + ChatGPT conclusions

project/reports/chatgpt/
= implementation-ready Codex task specifications

project/reports/codex/
= Codex execution and verification evidence
```

For detailed project entry flows and the recommended `AGENTS.md` collaboration block,
read `project-integration.md`.

## Standard loop

```text
User identifies project + invokes agent-collaboration
→ ChatGPT reads project AGENTS.md
→ ChatGPT reads canonical collaboration Skill/references
→ ChatGPT reads project concept index and only relevant concepts
→ ChatGPT reads project Skill/router as needed
→ User + ChatGPT design and decide
→ ChatGPT delegation decision
   ├─ ChatGPT-capable → ChatGPT performs + verifies directly
   └─ local-only / unavailable capability → continue below
→ durable concept update when needed
→ ChatGPT freezes executable decisions into project reports/chatgpt/
→ ChatGPT commits/pushes task
→ short Codex launch prompt
→ Codex repository synchronization
→ Codex local implementation/execution
→ Codex verification
→ Codex report in project reports/codex/ + commit/push
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

Project reports remain in the project that owns them:

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

- `agent-collaboration` is the shared collaboration authority for User, ChatGPT, and
  Codex.
- Project-specific work records remain in the owning project repository.
- User + ChatGPT own design; Codex executes the approved specification.
- ChatGPT delegates only when a required capability is unavailable to ChatGPT or
  materially local to the User's machine.
- ChatGPT freezes all reasonably determinable task decisions before Codex handoff.
- One formal Codex task is active at a time.
- The next formal Codex task starts only after independent audit of the previous task.
- Codex executes; ChatGPT accepts.
- Evidence, not self-reported PASS, determines completion.
- Scientific and product rigor is mandatory; engineering ceremony is not.
