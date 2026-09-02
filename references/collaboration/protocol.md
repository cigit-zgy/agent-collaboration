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

After that gate passes, choose the smallest sufficient execution mode.

### Routine local execution

Use routine local execution for bounded, ephemeral local work when all of these are true:

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

Use a formal delegated task when any of these materially applies:

- repository-changing work;
- a durable/shared dataset, runtime, external service/state, credential state, or another persistent resource must be changed;
- durable project artifacts must be created or changed;
- the task is long or multi-step enough to need a frozen specification;
- scientific, product, trust, security, or data-loss risk requires an auditable boundary;
- reproducibility, accountability, or later acceptance requires a durable evidence chain.

For a formal task, ChatGPT freezes the determinable scope, governing design/operational sources, affected area, required behavior, verification level, acceptance criteria, Git requirements, and expected report path.

Formal task format and launch block: `templates/chatgpt-task.md`.

## Collaboration loop

```text
User goal
→ inspect applicable authority/evidence
→ User + ChatGPT develop/adjudicate design
→ User accepts the project decision when final human authority is required
→ update design authority first when design changes
→ delegation gate
   ├─ connected capability sufficient → ChatGPT executes + verifies
   └─ local capability required
       ├─ routine local execution → Codex result → ChatGPT review
       └─ formal delegated task   → committed task → Codex execution/report
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

- User + ChatGPT develop/adjudicate the design; the User retains final decision authority.
- ChatGPT delegates only for a concrete unavailable/local capability.
- Routine execution is permitted only when persistent/shared mutation is excluded.
- Codex does not self-accept.
- Evidence determines technical acceptance.
- Formal ceremony is used only when the task requires a durable specification/evidence chain or persistent/shared mutation.
- Scientific/product rigor is mandatory; verification effort is risk-proportional.
