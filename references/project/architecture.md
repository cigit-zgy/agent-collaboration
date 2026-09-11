# Project architecture and integration contract

Load this reference for project ownership, authority surfaces, runtime reading routes, onboarding, and responsibility placement.

Normal multi-conversation resume/current state is owned by `current.md`. Existing-project migration is owned by `migration.md`. Governance/report layout is owned by `reports.md`. Concept history is owned by `concept.md`. Current living design is owned by `design.md` and lives under `reports/design/`.

## Project entry

Root `AGENTS.md` is the project-local constitution. It identifies project identity, authority, ownership boundaries, workflow entry, runtime/tooling authority, normal resume route, and genuine human/trust checkpoints.

## Responsibility-based architecture

Create only responsibilities with a real owner, artifact, and consumer.

Common pattern:

| Responsibility | Common path | Meaning |
|---|---|---|
| project constitution | `AGENTS.md` | repository-scoped authority/routing |
| current work edge | `CURRENT.md` | mutable NOW-state for multi-conversation work |
| current accepted design | `reports/design/` | canonical living design; one current set |
| design history/input | `reports/concept/` | chronological concept journal |
| delegated tasks | `reports/chatgpt/` | LOCAL-QUICK/FORMAL task specifications |
| FORMAL execution evidence | `reports/codex/` | Codex reports |
| exceptional conversation delta | `reports/handoff/` | residual continuity only |
| human orientation | `README.md` | human-facing intro |
| runtime/tooling authority | `pyproject.toml` or equivalent | dependencies/tooling |
| reusable implementation | `src/` | executable implementation |
| durable model/data objects | project-defined | canonical artifacts |
| mutable domain/run state | `workspace/` when used | scientific/application current state |
| tests | `tests/` | conformance/regression evidence |
| historical retention | `00_archive/` | repository-root history boundary |
| Agent ephemeral state | `tmp/` | project-owned scratch boundary |

`CURRENT.md` is not a substitute for domain `workspace/`.

## Design authority

For projects using explicit living design:

```text
reports/design/
```

is the single current accepted design authority.

```text
reports/concept/ = historical/exploratory design input
reports/design/  = current accepted design
CURRENT.md       = current work pointer only
registered source/evidence = model-specific scientific fact authority
```

`reports/design/` is not a chronological report family; its README/topic structure is owned by `design.md`.

## Runtime routes

Routine execution:

```text
AGENTS.md
→ declared workflow SKILL.md
→ owning reference/script
```

Normal conversation resume:

```text
AGENTS.md
→ CURRENT.md
→ reports/design/README.md when present
→ identify current concern
→ load only directly relevant owner(s)
```

This is orientation, not migration. Do not preload the whole design tree, concept history, old tasks/reports/handoffs, archive, or complete collaboration references.

Current design/conformance:

```text
AGENTS.md
→ reports/design/README.md
→ relevant current design topic(s)
→ affected Skill/reference projection
→ implementation/tests as needed
```

Existing-project collaboration migration:

```text
current collaboration SKILL.md
→ migration.md
→ target AGENTS + branch/HEAD/state
→ CURRENT.md when present
→ reports/design/README.md when present
→ only directly relevant anchors
→ migrate drift only
```

New project/major design:

```text
AGENTS.md
→ prior-art route
→ strongest relevant precedents
→ reports/concept note(s) when useful
→ User + ChatGPT adjudication
→ reports/design/ current-state update
→ operational projection
```

Historical design rationale:

```text
current reports/design topic
→ exact relevant reports/concept note(s) only when needed
```

Exceptional conversation-only recovery uses only the explicitly relevant handoff; do not traverse handoff history by default.

## Ownership boundaries

```text
current work edge              → CURRENT.md
current project design          → reports/design/
design history/input            → reports/concept/
reusable implementation         → implementation owner
mutable domain/run state         → workspace owner when used
exceptional conversation delta  → reports/handoff/
historical retained state       → 00_archive/
Agent ephemeral state           → tmp/ + execution contract
```

Concept notes become design only through User + ChatGPT adjudication and a concrete `reports/design/` update. CURRENT never becomes design authority.

## Project onboarding

```text
inspect repository
→ establish concise AGENTS.md
→ declare ownership/tooling boundaries
→ establish reports/design/ when explicit living design is needed
→ use reports/concept/ for design history/input
→ establish CURRENT.md only when resume cost justifies it
→ run prior-art gate for substantial new design
→ expose workflow Skill only when a repeatable Agent workflow exists
→ project reports/design/ into Skill/reference/code/tests
→ route execution through DIRECT / LOCAL-QUICK / FORMAL
```

Existing repositories upgrading from older collaboration layouts use `migration.md`. A root `design/` tree is migrated to `reports/design/` without changing project-specific semantics.

Do not create handoff merely because a project is long-running.

## Review criterion

A project architecture is sufficient when a fresh Agent can locate project authority, current work edge, current design owner, design-history route, workflow entry, source/scientific authority, migration route, archive/tmp boundaries, and the first next action without reconstructing the previous conversation.
