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
       └─ formal delegated task   → committed local-only spec → Codex execution/report
→ ChatGPT independent acceptance review
→ User retains final decision/override authority
```

## Concurrency

Independent local/formal tasks may run concurrently when their branches/worktrees and mutable resources are independent.

Tasks that share a branch, worktree, files, datasets, runtime state, external state, credentials, or another mutable resource require explicit coordination before concurrent execution.

If non-interference or exclusive ownership cannot be established, concurrent execution is not allowed; serialize the tasks.

Concurrency is therefore constrained by shared mutable state, not by an arbitrary single-task rule.

## Repository synchronization

These Git synchronization rules apply to formal repository-changing Codex tasks.

Before editing, Codex:

1. fetches remote state;
2. inspects branch, HEAD, upstream, and worktree;
3. preserves pre-existing User changes;
4. fast-forwards only when the branch is merely behind and the update is safe;
5. verifies task source and baseline before editing.

Divergence that requires merge/rebase/cherry-pick is an explicit reconciliation decision rather than implicit task permission.

After implementation Codex commits task-scoped changes, pushes, fetches again, verifies `HEAD == upstream` when safely achievable, and reports intentionally preserved pre-existing changes.

Routine read-only/local-inspection execution does not create Git ceremony merely because Codex is involved.

## Acceptance

Codex does not self-accept. ChatGPT independently reviews the evidence and issues the technical acceptance verdict:

```text
PASS | PASS WITH LIMITATIONS | BLOCKED | FAIL
```

The User retains final project/scientific/product decision and override authority.

## Stable collaboration artifacts

Formal tasks and reports use stable paths:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
reports/codex/YYMMDD_codex_NN.md
```

Project concepts use project-declared design paths such as `reports/concept/<topic>.md`.

Issued formal tasks and reports remain stable audit artifacts.

## Invariants

- The GitHub repository `cigit-zgy/agent-collaboration` is the canonical maintained collaboration source; local copies are optional caches.
- Formal tasks pin collaboration authority by repository + commit + path.
- Unresolved pinned authority is BLOCKED; similarly named local content is never an accepted substitute.
- User + ChatGPT develop/adjudicate the design; the User retains final decision authority.
- Delegation is per deliverable, not per task or file batch.
- ChatGPT completes all current-capability `DIRECT` deliverables before Codex handoff.
- Frozen DIRECT artifacts are read-only to Codex unless an explicit mechanical exception is declared.
- Codex owns only work with a concrete local/unavailable capability dependency.
- Routine execution is permitted only when persistent/shared mutation is excluded.
- Codex does not self-accept.
- Evidence determines technical acceptance.
- Formal ceremony is used only when the remaining local work requires a durable specification/evidence chain or persistent/shared mutation.
- Scientific/product rigor is mandatory; verification effort is risk-proportional.
