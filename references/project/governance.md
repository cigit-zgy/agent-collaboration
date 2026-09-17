# Project governance conformance contract

Load this reference only when changing project-governance artifacts, normalizing an existing repository, or when authority/artifact drift is suspected. It is not a mandatory preflight for every code edit.

## Purpose

Keep durable project information in the correct owner without turning governance into a second execution workflow.

## Core invariants

### One current Design

When living Design is used, `reports/design/` is the only current Design tree. Do not keep a parallel root `design/`, dated Design tree, backup/current alternative, or superseded current owner.

Self-hosting Skill/policy repositories may intentionally use `SKILL.md + references/` as current operational authority under `design.md`; do not duplicate the same semantics merely for symmetry.

### One concern, one owner

Each current Design concern has one primary owner. Cross-topic interfaces are allowed; duplicate semantic ownership is not.

If one bounded rule routinely needs several Design files just to establish its meaning, consolidate ownership before adding more Design structure. Topic-count guards live in `design.md` / `reconciliation.md`.

### Artifact admission

```text
accepted current project Design       → reports/design/ or declared self-hosting current owner
substantive ChatGPT historical work   → reports/chatgpt/
Codex execution records               → reports/codex/
explicit User-requested history       → reports/concept/
conversation-boundary continuity      → reports/handoff/
current work edge                     → CURRENT.md
maintained verification logic         → tests/
project-specific scientific/source/canonical artifacts
                                      → project-declared owner
```

Do not create `reports/verification/` or another family merely because evidence has a different test category.

### Historical Reports are append-only

`chatgpt`, `codex`, `concept`, and `handoff` records are never overwritten or repurposed. Later work gets a new dated artifact.

Current Design is different: it is replace-in-place current state.

### Concept creation is explicit

Create a Concept only when the User explicitly asks to persist material in Concept.

Each request creates a new dated `reports/concept/YYMMDD_concept_NN.md`; old Concepts are not overwritten or repurposed.

When a requested Concept records an accepted Design consequence, update the current Design owner in the same work unit.

### Conversation handoff is explicit

When the User explicitly replaces a long conversation, create one compact append-only handoff under `handoff.md`, update CURRENT to point to it, and return only the compact resume locator.

### CURRENT is NOW only

`CURRENT.md` points to the present work edge, relevant coordinates, latest handoff when applicable, a small number of open edges, and exactly one next action. It is not history, evidence, backlog, or a Design copy.

### Project-specific purity stays project-specific

Canonical-artifact contents, scientific object shapes, source/evidence rules, and publication-purity contracts belong to the project that owns those artifacts.

## Drift response

Repair deterministic governance drift directly when the correction does not choose new scientific/product meaning, for example obsolete parallel Design paths, wrong owner pointers, historical Reports used as current authority, CURRENT carrying history, or non-canonical report placement.

If cleanup would require choosing among conflicting scientific/product meanings, stop that semantic path for User + ChatGPT adjudication.

## Migration

Repository normalization should reduce structure rather than mechanically move it:

```text
identify real current owners
→ merge/remove duplicate authority
→ preserve historical work in append-only Reports
→ preserve project-specific artifacts with project-declared owners
→ establish one current Design tree when used
→ shrink CURRENT to present-state pointers
→ normalize report routing
→ update AGENTS/Skill pointers
```

Do not create Concepts merely to document cleanup unless the User explicitly requests Concept persistence.

## Completion

Governance conforms when an unfamiliar Agent can identify current authority and historical-record owners without reconstructing conversation history, one concern has one owner, current Design is singular, CURRENT is present-state only, and project-specific semantics remain with the project rather than generic collaboration policy.
