# Project architecture and integration contract

Load this reference for project ownership, authority surfaces, runtime routes, onboarding, and responsibility placement.

Normal resume is owned by `current.md`; repository conformance/admission by `governance.md`; current Design by `design.md`; accumulated report-to-Design synchronization by `reconciliation.md`.

## Project entry

Root `AGENTS.md` is the project-local constitution and routing surface.

## Responsibility map

| Responsibility | Common path | Meaning |
|---|---|---|
| project constitution | `AGENTS.md` | authority/routing |
| current work edge | `CURRENT.md` | mutable NOW-state |
| current accepted Design | `reports/design/` | one current normal form |
| ChatGPT historical work | `reports/chatgpt/` | tasks/direct/acceptance records |
| Codex historical execution | `reports/codex/` | concise LOCAL-QUICK + FORMAL records |
| explicit User-requested reasoning | `reports/concept/` | append-only Concept history |
| conversation boundary | `reports/handoff/` | compact session replacement record |
| scientific/model facts | project-defined owner | domain authority |
| runtime/tooling | `pyproject.toml` or equivalent | dependencies/mechanical tooling |
| mutable domain/run state | `workspace/` when used | scientific/application state |
| maintained verification | `tests/` | conformance/regression logic |
| historical retention | `00_archive/` | cold history only |
| Agent scratch | `tmp/` | ephemeral boundary |

Do not create `reports/verification/` merely to classify test evidence.

## Current versus historical

```text
current accepted semantics → reports/design/ or declared self-hosting current owner
historical work/evidence    → chatgpt / codex / concept / handoff
current edge                → CURRENT.md
```

Every current Design concern has one owner. A bounded concern normally needs one primary topic plus at most one necessary secondary topic.

## Runtime routes

Normal resume:

```text
AGENTS.md
→ CURRENT.md
→ one directly relevant current owner
```

When CURRENT points to a conversation handoff:

```text
AGENTS.md
→ CURRENT.md
→ that one handoff
→ one current owner as needed
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

## Design maintenance

Accepted Design consequences are written immediately in the same work unit.

`reconciliation.md` provides a backstop when accumulated Reports may contain missed Design deltas. Periodic reconciliation classifies only new reports since the cursor and never summarizes report history wholesale into Design.

## Concept boundary

Do not create Concept notes automatically. Only an explicit User request creates a new dated Concept. Any accepted Design consequence from that Concept is synchronized in the same work unit.

## Conversation boundary

When the User explicitly switches a long conversation, create one compact append-only handoff after accepted state/reports/CURRENT are durable. The next conversation reads only `AGENTS.md + CURRENT.md + that handoff` before loading the one relevant current owner.

## Existing-project migration

```text
current collaboration SKILL.md
→ migration.md + governance.md
→ target AGENTS/CURRENT/branch/HEAD
→ current Design map when present
→ reduce governance drift
→ migrate only the normalized current state
```

## New project / major design

```text
prior-art route when required
→ User + ChatGPT adjudication
→ current Design update
→ operational projection
→ append historical work records as appropriate
```

For projects using several reusable Skills, current Skill selection is owned by one Design topic such as `runtime_and_skills`; AGENTS routes to it rather than duplicating the profile.

## Onboarding

```text
inspect repository
→ establish concise AGENTS.md
→ establish real scientific/runtime owners
→ establish one current Design tree when explicit Design is needed
→ establish CURRENT.md only when resume cost justifies it
→ establish append-only ChatGPT/Codex report families
→ expose workflow Skills only for repeatable workflows
→ project current Design into Skill/reference/code/tests
```

## Review criterion

A project architecture is sufficient when a fresh Agent can locate current authority, work edge, Design owner, historical work records, scientific fact owner, workflow entry, and first next action without reconstructing prior conversations.
