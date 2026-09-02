# Collaboration protocol

This contract governs the User ↔ ChatGPT ↔ Codex collaboration loop.

## Roles

### User

The User defines goals and constraints, makes genuine human scientific/product decisions, and authorizes exceptional scope or trust-boundary changes.

### ChatGPT

ChatGPT is the design partner, remote-capable executor, formal task author, independent auditor, and acceptance authority. It inspects current evidence before delegation and resolves every decision that can reasonably be resolved without local-only capability.

When connected capabilities are sufficient, ChatGPT performs and verifies the work directly.

### Codex

Codex is the local executor for work that genuinely requires local-machine capability, such as local worktree state, CLI/runtime execution, builds/tests/rendering, credentials, machine-local services, or another capability unavailable to ChatGPT.

Codex executes the committed specification and reports contradictions, missing prerequisites, or unresolved human decisions instead of silently redesigning approved behavior.

## Project authority

Project-specific precedence comes from the applicable project `AGENTS.md`. Maintained scientific projects may declare `reports/concept/` as canonical User + ChatGPT design authority; see `../project/concept.md` and `../project/architecture.md`.

```text
project concept
→ Skill/reference operational projection
→ implementation
→ tests
→ runtime artifacts
```

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

A Codex task requires a concrete local or otherwise unavailable capability. When delegation is justified, ChatGPT freezes the determinable scope, governing design/operational sources, affected area, required behavior, verification level, acceptance criteria, Git requirements, and report path.

Formal task format: `templates/chatgpt-task.md`.

## Collaboration loop

```text
User goal
→ inspect applicable authority/evidence
→ User + ChatGPT decide design
→ update design authority first when design changes
→ delegation gate
   ├─ connected capability sufficient → ChatGPT executes + verifies
   └─ local capability required       → committed Codex task
→ Codex safe synchronization + execution + specified verification
→ Codex report
→ ChatGPT independent audit
→ PASS | PASS WITH LIMITATIONS | BLOCKED | FAIL
```

Only one formal Codex task is active at a time; the next task starts after independent audit of the previous one.

## Repository synchronization

Before local implementation Codex:

1. fetches remote state;
2. inspects branch, HEAD, upstream, and worktree;
3. preserves pre-existing User changes;
4. fast-forwards only when the branch is merely behind and the update is safe;
5. verifies task source and baseline before editing.

Divergence that requires merge/rebase/cherry-pick is an explicit reconciliation decision rather than an implicit task permission.

After implementation Codex commits task-scoped changes, pushes, fetches again, verifies `HEAD == upstream` when safely achievable, and reports intentionally preserved pre-existing changes.

## Stable collaboration artifacts

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
reports/codex/YYMMDD_codex_NN.md
reports/concept/<topic>.md
```

Issued formal tasks and reports remain stable audit artifacts.

## Acceptance invariants

- User + ChatGPT own design; Codex executes approved local work.
- ChatGPT delegates only for a concrete unavailable/local capability.
- Codex does not self-accept.
- Evidence determines acceptance.
- Scientific/product rigor is mandatory; verification effort is risk-proportional.
