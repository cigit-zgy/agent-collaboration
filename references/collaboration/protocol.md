# Collaboration protocol

This contract governs the User ↔ ChatGPT ↔ Codex collaboration loop.

## Roles

### User

The User defines goals and constraints, makes genuine human scientific/product decisions, authorizes exceptional scope or trust-boundary changes, and retains final decision/override authority.

### ChatGPT

ChatGPT is the design partner, remote-capable executor, task author, and independent acceptance reviewer. It inspects current evidence before delegation, resolves every decision that can reasonably be resolved without local-only capability, and issues an evidence-based technical verdict after delegated work.

When connected capabilities are sufficient, ChatGPT performs and verifies the work directly.

### Codex

Codex is the local executor for work that genuinely requires local-machine capability, such as local worktree state, CLI/runtime execution, builds/tests/rendering, credentials, machine-local services, or another capability unavailable to ChatGPT.

Codex executes the supplied scope and reports contradictions, missing prerequisites, or unresolved human decisions instead of silently redesigning approved behavior.

## Collaboration authority source

The canonical maintained source for this collaboration standard is the GitHub repository:

```text
cigit-zgy/agent-collaboration
```

No machine-local installation or checkout of `agent-collaboration` is assumed.

A formal task that depends on this collaboration standard must pin the exact authority it was authored against using:

```text
repository + commit SHA + repository-relative path
```

Resolution order for Codex is:

```text
1. exact verified local checkout at the pinned repository + commit, if one already exists
2. otherwise fetch/read the exact pinned files from GitHub
3. if the pinned authority cannot be resolved, BLOCKED
```

A local checkout is only a cache. It is not an authority merely because its filenames look similar or it has its own upstream.

Codex must not substitute:

```text
an older local clone
another Skill
similarly named files
a guessed renamed path
an inferred "equivalent" policy
```

for an unresolved pinned collaboration path.

If a task cites an invalid machine-local collaboration path but also identifies an unambiguous pinned GitHub repository/commit/path, use the pinned GitHub authority and report the stale local path as a task-authoring defect. If no pinned GitHub authority exists, stop rather than infer replacements.

ChatGPT may inspect current `master` while authoring a task, but Codex executes against the task-pinned commit so collaboration policy cannot drift during execution.

## Project authority

Project-specific precedence comes from the applicable project `AGENTS.md`. Maintained scientific projects may declare `reports/concept/` as canonical project design authority; see `../project/concept.md` and `../project/architecture.md`.

Project design authority remains separate from registered source/evidence authority for model-specific scientific facts.

## Reading modes

Routine execution:

```text
project AGENTS.md
→ declared workflow SKILL.md
→ owning sub-Skill
→ required reference/script
```

Design, redesign, or conformance audit:

```text
project AGENTS.md
→ reports/concept/README.md
→ relevant governing concept
→ affected Skill/reference
→ implementation/tests as needed
```

## Delegation gate

Codex is used only when ChatGPT can name a concrete local or otherwise unavailable capability.

Passing this task-level gate does **not** transfer every deliverable in the task to Codex. Delegation is decided per deliverable.

### Deliverable-level capability partition

Before issuing any Codex instruction, ChatGPT partitions the requested outputs into:

```text
DIRECT
= ChatGPT can complete the deliverable with current connected capabilities
  without requiring local-only evidence or execution

LOCAL
= the deliverable genuinely requires local worktree/runtime/filesystem/build/test/
  rendering/credential/service capability unavailable to ChatGPT
```

The governing rule is:

```text
DIRECT deliverable
→ ChatGPT completes + verifies it before handoff

LOCAL deliverable
→ Codex may own its local execution/implementation
```

A repository-changing task may contain both classes. Repository mutation by itself is not a reason to delegate a particular deliverable when ChatGPT can already make that change directly.

For maintained projects, the following are presumed `DIRECT` when ChatGPT has connected repository read/write access:

- canonical concept/design documents;
- root or nested `AGENTS.md` authoring;
- `SKILL.md` authoring;
- `references/*.md` operational-contract authoring;
- task specifications and other substantive design/projection documentation.

These files may be inputs to Codex implementation, but Codex does not receive substantive design/projection authorship merely because the same task also contains local Python, tests, CLI, packaging, or runtime work.

An exception is allowed only when a normally direct-capable deliverable is inseparable from a local-only fact or generated result and introduces no new design semantics. The formal task must name that local-only dependency explicitly and constrain the edit mechanically.

Before formal handoff, every `DIRECT` deliverable in scope must already be committed/pushed or otherwise completed through the connected authority. The Codex task then starts from those artifacts as frozen inputs.

### Frozen DIRECT inputs are read-only to Codex

Every DIRECT artifact listed as completed before handoff is immutable for the duration of the delegated task unless the task explicitly grants a narrowly mechanical exception.

Codex must not substantively edit, delete, rename, reformat, regenerate, or replace a frozen DIRECT artifact. In particular, frozen concept files, `AGENTS.md`, `SKILL.md`, and `references/*.md` are read-only implementation authority when ChatGPT completed them before handoff.

If local implementation reveals that a frozen DIRECT artifact is incomplete, contradictory, or impractical, Codex stops the affected work and reports the exact conflict. It does not repair the design/projection itself. ChatGPT reopens and updates the DIRECT artifact separately, the User accepts any required design change, and local implementation resumes only from the updated frozen input.

A mechanical exception is valid only when the formal task names the exact file, exact permitted transformation, and local-only dependency, and the edit cannot introduce or reinterpret design semantics.

If a requested Codex deliverable lacks a concrete local-only reason, remove it from Codex scope and complete it directly instead.

### Routine local execution

After the capability partition, use routine local execution for bounded, ephemeral `LOCAL` work when all of these are true:

```text
no intended mutation of repository state
AND no intended mutation of durable/shared datasets
AND no intended mutation of persistent runtime state
AND no intended mutation of external mutable/service state
AND no intended mutation of credential state
AND no intended mutation of any other persistent/shared resource
AND no durable project artifact is required
AND no design/scientific/trust decision is delegated
AND no audit chain is required
AND the task can be understood from a direct instruction
```

Typical examples include reproducing a bug, running a focused test, inspecting an environment, checking a local file/state, or gathering diagnostic evidence without persistent/shared mutation.

Route:

```text
direct Codex instruction
→ local result/evidence
→ ChatGPT review
```

Routine local execution does not require a committed ChatGPT task or Codex report unless the work discovers a reason to escalate.

If every routine predicate cannot be established, use the formal path when its scope can be safely specified; otherwise stop and surface the unresolved boundary.

### Formal delegated task

Use a formal delegated task for the `LOCAL` partition when any of these materially applies:

- repository-changing local implementation is required;
- a durable/shared dataset, runtime, external service/state, credential state, or another persistent resource must be changed;
- durable local project artifacts must be created or changed;
- the local work is long or multi-step enough to need a frozen specification;
- scientific, product, trust, security, or data-loss risk requires an auditable boundary;
- reproducibility, accountability, or later acceptance requires a durable evidence chain.

For a formal task, ChatGPT first completes all `DIRECT` deliverables, then freezes the remaining local scope, governing design/operational sources, affected area, required behavior, verification level, acceptance criteria, Git requirements, and expected report path.

Formal task format and launch block: `templates/chatgpt-task.md`.

## Formal handoff state

A formal repository-changing task has two distinct Git reference points:

```text
design/projection baseline
= the commit after the DIRECT design/projection artifacts are complete
  and before the formal task artifact is added

task/handoff commit
= the commit that contains the issued formal task and therefore represents
  the exact repository state Codex must reach before implementation begins
```

`baseline_sha` in the task describes the design/projection baseline. The containing task commit is supplied separately in the launch block because a file cannot contain the SHA of the commit that contains itself.

Codex start discipline is therefore:

```text
fetch
→ verify branch/worktree safety
→ reach the exact task/handoff commit by safe synchronization
→ verify the task source and frozen DIRECT inputs
→ only then begin LOCAL implementation
```

Codex must not begin from an earlier design baseline merely because the task file is visible remotely.

## Handoff branch freeze

Once the User launches a formal Codex task or Codex reports that execution has begun, the handed-off branch is frozen for overlapping ChatGPT/User repository writes until that execution is completed or explicitly aborted.

The default serialized flow is:

```text
ChatGPT completes DIRECT artifacts
→ ChatGPT commits formal task
→ Codex executes LOCAL work on the handed-off branch
→ Codex pushes/fetches/verifies
→ ChatGPT performs acceptance
→ branch is available for the next coordinated change
```

During active execution, ChatGPT must not advance the same branch with task-relevant or frozen-input changes merely because the changed files appear non-overlapping. A same-branch remote advance can force an otherwise successful local implementation into avoidable divergence and reconciliation.

If a DIRECT artifact or task specification must change after Codex has started:

```text
stop/abort or explicitly supersede the active task
→ preserve Codex/User local state
→ ChatGPT updates and commits the DIRECT artifact
→ issue a new task/handoff commit or explicit resumed task
→ Codex continues only from the new coordinated handoff
```

Independent work may still proceed concurrently on a separate branch/worktree when non-interference is established under the concurrency rules below.

## Upstream/downstream ownership boundary

A task owns only the stage/module/contracts explicitly included in its scope.

If an in-scope upstream contract change reveals that an out-of-scope downstream consumer is stale, the executor must report the downstream drift rather than silently migrate the downstream consumer.

Default rule:

```text
make the current owner correct
→ verify the current owner against its accepted contract
→ report downstream incompatibility
→ stop at the ownership boundary
```

Unless the formal task explicitly includes downstream migration, Codex must not:

- edit downstream stages merely to restore repository-wide compatibility;
- add compatibility shims that preserve a rejected upstream contract;
- reintroduce removed fields/files/interfaces for an old consumer;
- broaden scope only to make unrelated full-repository tests green.

A focused stage may therefore be accepted while later stages are explicitly reported as drift, provided the current stage satisfies its own contract and the task did not promise whole-pipeline compatibility.

Repository-wide checks that fail solely because an intentionally pending downstream owner still targets the old contract are evidence of downstream drift, not automatic failure of the completed upstream stage. The report must identify the affected consumer and the stale assumption precisely.

## Collaboration loop

```text
User goal
→ inspect applicable authority/evidence
→ User + ChatGPT develop/adjudicate design
→ User accepts the project decision when final human authority is required
→ update design authority first when design changes
→ partition deliverables: DIRECT | LOCAL
→ ChatGPT completes/verifies DIRECT deliverables
→ freeze DIRECT artifacts as Codex read-only inputs
→ local-capability gate for remaining LOCAL work
   ├─ no LOCAL work remains → ChatGPT completes task directly
   └─ LOCAL work remains
       ├─ routine local execution → Codex result → ChatGPT review
       └─ formal delegated task
          → committed local-only specification
          → task/handoff commit
          → handoff branch freeze
          → Codex execution/report
→ ChatGPT independent acceptance review
→ User retains final decision/override authority
```

## Concurrency

Independent local/formal tasks may run concurrently when their branches/worktrees and mutable resources are independent.

Tasks that share a branch, worktree, files, datasets, runtime state, external state, credentials, or another mutable resource require explicit coordination before concurrent execution.

An active formal handoff freezes its handed-off branch for overlapping repository writes even when another actor believes the paths are non-overlapping. Use a separate branch/worktree for genuinely independent concurrent work or serialize the changes.

If non-interference or exclusive ownership cannot be established, concurrent execution is not allowed; serialize the tasks.

Concurrency is therefore constrained by shared mutable state, not by an arbitrary single-task rule.

## Repository synchronization

These Git synchronization rules apply to formal repository-changing Codex tasks.

Before editing, Codex:

1. fetches remote state;
2. inspects branch, HEAD, upstream, and worktree;
3. preserves pre-existing User changes;
4. fast-forwards only when the branch is merely behind and the update is safe;
5. reaches and verifies the exact task/handoff commit;
6. verifies the task source, declared baseline, and frozen DIRECT inputs before editing.

Divergence that requires merge/rebase/cherry-pick is an explicit reconciliation decision rather than implicit task permission.

After implementation Codex commits task-scoped changes, pushes, fetches again, verifies `HEAD == upstream` when safely achievable, and reports intentionally preserved pre-existing changes.

Routine read-only/local-inspection execution does not create Git ceremony merely because Codex is involved.

## Acceptance

Codex does not self-accept. ChatGPT independently reviews the evidence and issues the technical acceptance verdict:

```text
PASS | PASS WITH LIMITATIONS | BLOCKED | FAIL
```

A scoped implementation may receive `PASS WITH LIMITATIONS` when its own acceptance criteria are satisfied but explicitly out-of-scope downstream drift or unavailable optional external verification remains. Such limitations must not be used to hide an in-scope contract failure.

The User retains final project/scientific/product decision and override authority.

## Stable collaboration artifacts

Formal tasks and reports use stable paths:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
reports/codex/YYMMDD_codex_NN.md
```

Issued task/report artifacts remain durable evidence and are not silently rewritten into later state. If a task is superseded, preserve it and issue a new task artifact that names the superseded task explicitly.
