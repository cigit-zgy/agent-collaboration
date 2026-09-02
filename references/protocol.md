# Collaboration protocol

This file is the current operational authority for the User ↔ ChatGPT ↔ Codex
collaboration loop.

## Roles

### User

- defines goals and constraints;
- makes genuine human scientific/product decisions;
- approves exceptional scope or trust-boundary changes.

### ChatGPT

ChatGPT is the design partner, remote-capable executor, formal task author, independent
auditor, and acceptance authority.

Before delegation, ChatGPT must inspect current repository evidence, resolve every
design decision that can reasonably be resolved, and decide whether local execution
is actually required.

If ChatGPT can safely and completely perform the work with its connected tools, it
does the work directly and verifies the result. Do not create a Codex task merely to
offload effort.

### Codex

Codex is the local executor for committed tasks that genuinely require local-machine
capability: local worktree state, CLI/runtime execution, builds/tests/rendering,
credentials or machine-local services, or another capability unavailable to ChatGPT.

Codex executes the committed specification. It may report contradictions, infeasible
instructions, missing prerequisites, or unresolved human decisions, but it must not
silently redesign approved behavior, architecture, scientific/product semantics, or
scope.

## Project authority and entry

Project-specific instructions come from the applicable project `AGENTS.md`.
A project may declare its Agent-facing workflow Skill at any repository-relative
path; do not assume `project/SKILL.md`.

A maintained scientific/research project may also declare selected
`reports/concept/*` topics as canonical User + ChatGPT design authority. When it does,
use the hierarchy defined by `report-concept-policy.md` and `project-integration.md`:

```text
project design concept
→ Skill/reference operational projection
→ implementation
→ tests
→ runtime artifacts
```

The operational projection must conform to the governing design concept; it may not
silently redefine it. Project design authority remains distinct from registered
source/evidence authority for model-specific scientific facts.

## Two project reading modes

### Ordinary runtime

Prefer the short route:

```text
applicable project AGENTS.md
→ declared project workflow SKILL.md
→ owning sub-Skill
→ only references/scripts required by the active branch
```

A design-authority concept does not need to be loaded during every routine run when a
current operational projection already exists.

### Design/redesign/conformance audit

If the task changes accepted architecture/scientific semantics, rebuilds a stage from
its agreed design, or audits projection/implementation drift:

```text
project AGENTS.md
→ reports/concept/README.md
→ only relevant design-authority concept topic(s)
→ affected Skill/reference projection
→ implementation/tests as needed
```

Load `agent-collaboration/SKILL.md` and this protocol when collaboration/handoff
rules are needed.

## Delegation gate

Before issuing a Codex task, ChatGPT must answer:

> Which concrete local or otherwise unavailable capability requires Codex?

If no concrete answer exists, do not delegate.

When delegation is required, ChatGPT freezes every reasonably determinable decision:

- exact scope and non-goals;
- governing project design concept(s), when applicable;
- authoritative operational references/projections;
- affected files/areas;
- required behavior and boundaries;
- verification level and acceptance criteria;
- Git requirements;
- expected Codex report path and fixed stdout.

Use `chatgpt-task-template.md` for the formal specification.

## Standard collaboration loop

For ordinary implementation work:

```text
User identifies project and goal
→ ChatGPT reads applicable AGENTS.md
→ ChatGPT follows the project's declared authority model
→ ChatGPT reads the minimum required design concept and/or operational projection
→ User + ChatGPT design and decide
→ when design changes, update governing design authority first
→ delegation gate
   ├─ ChatGPT-capable → ChatGPT performs + verifies directly
   └─ local/unavailable capability → committed Codex task
→ Codex safe Git synchronization
→ local execution + specified verification
→ Codex report
→ ChatGPT independent audit
→ PASS | PASS WITH LIMITATIONS | BLOCKED | FAIL
→ update design concept only if User + ChatGPT accepted a design change
→ update decision-history concepts only when rationale/history changed
```

Only one formal Codex task is active at a time. The next task begins only after
independent audit of the previous one.

## Repository synchronization

Before local implementation Codex must:

1. `git fetch`;
2. inspect branch, `HEAD`, upstream, and worktree;
3. preserve pre-existing User changes;
4. fast-forward only when the branch is merely behind and doing so is safe;
5. stop rather than invent a merge/rebase when divergence or dirty state makes the
   update unsafe;
6. verify task source/baseline consistency before editing.

A formal task never authorizes `reset --hard`, force-push, destructive cleanup, or
an invented merge/rebase.

After implementation Codex must:

1. commit all task-scoped changes;
2. push to the configured upstream;
3. fetch again;
4. verify `HEAD == upstream` when safely achievable;
5. report intentionally preserved pre-existing changes.

## Reports and concepts

Use stable paths:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
reports/codex/YYMMDD_codex_NN.md
reports/concept/<topic>.md
```

Issued formal tasks and Codex reports are stable audit artifacts. Do not move or
rewrite them later merely for calendar-based organization.

Concept role is project-declared:

- `decision_history`: rationale/history that points to current operational authority;
- `design_authority`: canonical User + ChatGPT project design specification whose
  downstream Skills/references/code/tests must conform.

The `agent-collaboration` repository itself uses `decision_history`; maintained water
research projects normally use selected design-authority concepts for their accepted
scientific/architectural plans.

## Invariants

- User + ChatGPT design; Codex executes approved local work.
- ChatGPT delegates only for a concrete unavailable/local capability.
- Codex does not self-accept.
- Evidence, not self-reported PASS, determines acceptance.
- This repository's current operational rules live in `references/*`.
- A project may declare concept topics as canonical design authority; operational
  projections must conform and cannot silently override them.
- Project design authority and model/source scientific fact authority are distinct.
- Project workflow Skill paths are project-declared.
- Formal task/report paths remain stable after issue.
- Scientific/product rigor is mandatory; engineering ceremony is risk-proportional.
