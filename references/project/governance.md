# Project governance conformance contract

Load this reference only when changing project-governance artifacts, normalizing an existing repository, or when authority/artifact drift is suspected. It is not a mandatory preflight for every code edit.

## Purpose

Keep durable project information in the correct owner without turning governance into a second execution workflow.

## Core invariants

### One current Design

When living Design is used, `reports/design/` is the only current Design tree. Do not keep a parallel root `design/`, dated Design tree, backup/current alternative, or superseded current owner.

### One concern, one owner

Each current Design concern has one primary owner. Cross-topic interfaces are allowed; duplicate semantic ownership is not.

If one bounded rule routinely needs several Design files just to establish its meaning, consolidate ownership before adding more Design structure.

### Artifact admission

```text
accepted current project Design       → reports/design/
explicit User-requested history       → reports/concept/
delegated Codex task                  → reports/chatgpt/
FORMAL execution evidence             → reports/codex/
current work edge                     → CURRENT.md
exceptional conversation-only delta   → reports/handoff/
project-specific scientific/source/canonical artifacts
                                      → project-declared owner
```

Do not use one artifact class as a convenient container for another responsibility.

### Concept creation is explicit

Create a Concept only when the User explicitly asks to persist material in Concept.

Each request creates a new dated `reports/concept/YYMMDD_concept_NN.md`; old Concepts are not overwritten or repurposed.

When a requested Concept records an accepted Design consequence, update the current `reports/design/` owner in the same work unit. Concept is history; Design is current state.

### CURRENT is NOW only

`CURRENT.md` points to the present work edge, relevant coordinates, a small number of open edges, and the next action. It is not a project history, evidence store, backlog, or Design copy.

### Project-specific purity stays project-specific

Canonical-artifact contents, scientific object shapes, source/evidence rules, and publication-purity contracts belong to the project that owns those artifacts.

Generic collaboration governance may require clear ownership and prevent duplicate authority, but it must not embed another project's file list, schema, model names, or scientific layout.

## Drift response

Repair deterministic governance drift directly when the correction does not choose new scientific/product meaning, for example obsolete parallel Design paths, wrong owner pointers, Concept used as current authority, CURRENT carrying historical detail, or non-canonical report placement.

If cleanup would require choosing among conflicting scientific/product meanings, stop that semantic path for User + ChatGPT adjudication.

## Migration

Repository normalization should reduce structure rather than mechanically move it:

```text
identify real current owners
→ merge/remove duplicate authority
→ preserve project-specific artifacts with project-declared owners
→ establish one reports/design/ tree when used
→ shrink CURRENT to present-state pointers
→ normalize task/report routing
→ update AGENTS/Skill pointers
```

Do not create Concepts merely to document cleanup unless the User explicitly requests Concept persistence.

## Completion

Governance conforms when an unfamiliar Agent can identify current authority and artifact owners without reconstructing history, one concern has one owner, current Design is singular, CURRENT is present-state only, and project-specific semantics remain with the project rather than generic collaboration policy.
