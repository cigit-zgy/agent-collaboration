# Project architecture and integration contract

Load this reference for project ownership, authority surfaces, runtime routes, onboarding, and responsibility placement.

Normal resume is owned by `current.md`; repository conformance/admission by `governance.md`; migration by `migration.md`; current Design by `design.md`; explicit User-requested Concept history by `concept.md`.

## Project entry

Root `AGENTS.md` is the project-local constitution and routing surface.

Before the first substantive repository-changing ChatGPT write, apply the bounded governance conformance gate from `governance.md` to the implicated authority surfaces.

## Responsibility map

| Responsibility | Common path | Meaning |
|---|---|---|
| project constitution | `AGENTS.md` | authority/routing |
| current work edge | `CURRENT.md` | mutable NOW-state |
| current accepted Design | `reports/design/` | one current living set |
| explicit User-requested design history | `reports/concept/` | append-only Concept artifacts |
| delegated tasks | `reports/chatgpt/` | LOCAL-QUICK/FORMAL task specs |
| FORMAL execution evidence | `reports/codex/` | Codex reports |
| exceptional conversation delta | `reports/handoff/` | residual continuity only |
| scientific/model facts | project-defined source/model/golden owner | domain authority |
| runtime/tooling | `pyproject.toml` or equivalent | dependencies/mechanical tooling |
| mutable domain/run state | `workspace/` when used | scientific/application state |
| tests | `tests/` | conformance/regression evidence |
| historical retention | `00_archive/` | history only |
| Agent scratch | `tmp/` | ephemeral boundary |

## Design authority

```text
reports/design/  = current accepted project Design
reports/concept/ = explicit User-requested historical reasoning only
CURRENT.md       = current work pointer only
source/model/golden owner = model-specific scientific facts/evidence
```

Every current Design concern has one owner. A bounded concern normally needs one primary topic plus at most one necessary secondary topic.

## Runtime routes

Normal resume:

```text
AGENTS.md
→ CURRENT.md
→ reports/design/README.md
→ one directly relevant owner
```

Routine execution:

```text
AGENTS.md
→ workflow SKILL.md
→ owning reference/script
```

Current Design/conformance:

```text
AGENTS.md
→ reports/design/README.md
→ one primary current topic
→ at most one necessary secondary topic
→ projection / implementation / tests
```

Historical rationale is not a normal runtime route. Read an exact Concept only when specifically needed.

## Concept boundary

Do not create Concept notes automatically during design/execution work.

Only an explicit User request creates a new dated Concept. That same work unit updates current `reports/design/` to the accepted consequence.

## Existing-project migration

```text
current collaboration SKILL.md
→ migration.md + governance.md
→ target AGENTS/CURRENT/branch/HEAD
→ current Design map when present
→ reduce governance drift
→ migrate only the normalized current state
```

Migration reduces duplicate/superseded current owners and overloaded status/history surfaces before declaring conformance.

## New project / major design

```text
prior-art route when required
→ User + ChatGPT adjudication
→ reports/design/ current-state update
→ optional Concept only if the User explicitly requests it
→ operational projection
```

## Onboarding

```text
inspect repository
→ establish concise AGENTS.md
→ establish real scientific/runtime owners
→ establish one reports/design/ tree when explicit Design is needed
→ establish CURRENT.md only when resume cost justifies it
→ expose workflow Skill only for a repeatable workflow
→ project Design into Skill/reference/code/tests
```

## Review criterion

A project architecture is sufficient when a fresh Agent can locate project authority, current work edge, current Design owner, scientific fact owner, workflow entry, migration/governance route, and first next action without reconstructing the previous conversation or loading historical Concepts.
