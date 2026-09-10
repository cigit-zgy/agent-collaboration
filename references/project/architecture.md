# Project architecture and integration contract

Load this reference for project repository ownership, authority surfaces, runtime reading routes, onboarding, and responsibility placement.

Normal multi-conversation resume/current work state is owned by `current.md`. Existing-project migration is owned by `migration.md`. Report-family/archive layout is owned by `reports.md`. Concept-journal semantics are owned by `concept.md`. Current living-design structure is owned by `design.md`. Exceptional conversation-only continuity is owned by `handoff.md`. External CLI/API/schema integration is owned by `external-tools.md`. Detailed local Git/worktree/tmp execution is owned by `../collaboration/execution.md`.

## Project entry

Root `AGENTS.md` is the project-local constitution. It identifies project identity, authority, ownership boundaries, workflow entry, runtime/tooling authority, normal resume route when used, and genuine human/trust checkpoints.

Use `../collaboration/agents.md` plus `templates/agents.md` when authoring it.

A project workflow Skill may live at any project-declared path; it is not required to be repository-root `SKILL.md`.

## Responsibility-based architecture

There is no universal canonical project filesystem beyond collaboration-wide hard contracts such as project reports, living-design semantics when used, and root archive rules. Create only responsibilities with a real owner, artifact, and consumer.

Common patterns include:

| Responsibility | Common path | Meaning |
|---|---|---|
| project constitution | `AGENTS.md` | repository-scoped authority and routing |
| current work edge | `CURRENT.md` | mutable NOW-state/pointers for long-running multi-conversation work |
| current accepted design | `design/` | canonical living design; one current set only |
| design exploration/history | `reports/concept/` | chronological concept journal; non-authoritative |
| human orientation | `README.md` | human-facing introduction/quick start |
| runtime/tooling authority | `pyproject.toml` or equivalent | dependencies, mechanical style, tooling |
| Agent capability package | `<agent-name>/` | project-owned workflow/sub-Skills when present |
| reusable implementation | `src/` | reusable executable code/infrastructure |
| durable model artifacts | `models/` | project-adopted model-specific artifacts |
| canonical reusable data | `data/` | project-adopted datasets |
| mutable run/domain state | `workspace/` | project-specific current case/model/runtime state |
| controlled investigations | `experiments/` | reproducible calibration/simulation/benchmark/case-study work |
| conformance/regression checks | `tests/` | tests for stable contracts/implementation |
| human technical documentation | `docs/` | durable explanation beyond README |
| publication assets | `manuscript/` | manuscript/figure/supplement materials when owned here |
| delegated tasks | `reports/chatgpt/` | durable LOCAL-QUICK/FORMAL specifications |
| Codex execution evidence | `reports/codex/` | FORMAL execution/verification reports |
| exceptional conversation delta | `reports/handoff/` | residual continuity only; not normal resume state |
| historical retention | `00_archive/` | single repository-root history boundary; never active authority |
| Agent-local temporary state | `tmp/` | project-owned ephemeral boundary |

`CURRENT.md` is not a substitute for domain `workspace/`. CURRENT tracks the collaboration/work edge; workspace may own real scientific/application mutable objects.

If `reports/` exists, its allowed direct children, filename contract, common metadata envelope, handoff placement, and archive rules are defined by `reports.md`.

## Design authority

For projects maintaining explicit architecture/design, canonical current design lives in:

```text
design/
```

`design.md` owns dynamic topic decomposition, current-only semantics, filename/identity rules, and projection order.

The authority relationship is:

```text
reports/concept/ = historical/exploratory design input
design/          = current accepted project design authority
CURRENT.md       = current work pointer only
registered source/evidence = model-specific scientific fact authority
```

Before a new project, core subsystem, major algorithm/architecture, or comparable gate-triggered design is accepted into `design/`, complete `prior-art.md`.

## Runtime reading routes

Expose the shortest stable route for routine operation:

```text
AGENTS.md
→ declared workflow SKILL.md
→ owning sub-Skill/reference/script
```

Do not force ordinary execution through project history when the operational projection is already stable.

### Normal conversation resume

For a mature long-running project using `CURRENT.md`:

```text
AGENTS.md
→ CURRENT.md
→ design/README.md when present
→ identify current concern
→ read only the directly relevant current owner(s)
```

This is orientation, not project migration. Do not preload the full design tree, concept history, old tasks/reports, old handoffs, archive, or complete collaboration references.

If `CURRENT.md` points to an active task/report/design owner, read that exact artifact only when it is needed to continue the current edge.

Before the first substantive repository-changing ChatGPT write, resolve current collaboration authority once under the collaboration refresh rule. The refresh does not justify unrelated preload.

### Existing-project migration

When a repository itself must be migrated to a newer collaboration model:

```text
current collaboration SKILL.md
→ migration.md
→ target project AGENTS.md + current branch/HEAD/state
→ design/README.md when present
→ CURRENT.md when present
→ only directly relevant current design/history/task/report anchors
→ migrate only drifted surfaces
```

Project-policy migration and normal conversation resume are different operations. A new conversation replacing a full old conversation does not by itself trigger migration.

### Current design / conformance

```text
AGENTS.md
→ design/README.md
→ directly relevant current design topic(s)
→ affected Skill/reference projection
→ implementation/tests as needed
```

### New project / major design

```text
AGENTS.md
→ current agent-collaboration prior-art route
→ strongest relevant external precedents
→ reports/concept note(s) when useful
→ User + ChatGPT adjudication
→ design/ current-state update
→ operational projection
```

### Historical design rationale

```text
current design topic
→ only exact relevant reports/concept note(s) when needed
```

### Exceptional conversation-only recovery

Use `reports/handoff/` only when meaningful continuity cannot reasonably be represented in current repository-native owners.

```text
AGENTS.md
→ CURRENT.md when present
→ newest explicitly relevant handoff only
→ current authority/state
```

Do not read historical handoff chains by default.

### External tool integration

When the active concern is an evolving external CLI/API/schema/parser/simulator interface, route directly from collaboration `SKILL.md` to `external-tools.md`.

## Ownership boundaries

```text
current collaboration/work edge → CURRENT.md
current project design           → design/ owner
design exploration/history       → reports/concept owner
reusable engine/algorithm/API     → reusable implementation owner
model-specific durable object    → model-artifact owner
canonical reusable dataset       → data owner
mutable domain/run state          → workspace owner
controlled investigation         → experiment owner
exceptional conversation delta   → handoff owner
historical retained state        → root 00_archive owner
Agent-created ephemeral state    → project tmp boundary + collaboration execution owner
```

Promotion between responsibilities is explicit. Concept notes become design only through User + ChatGPT adjudication and a concrete `design/` update. `CURRENT.md` never promotes itself into design authority. Experiment outputs become canonical data/model artifacts only after project adoption with provenance.

## Project-local ephemeral boundary

`tmp/` is the canonical project-owned location for Agent-created local ephemeral state. Detailed placement, `WORK_ID`, linked-worktree, cleanup, and Git-safety semantics are owned by `../collaboration/execution.md`.

## Project onboarding

```text
inspect actual repository
→ establish concise project AGENTS.md
→ declare real ownership + runtime/tooling boundaries
→ apply reports/archive hard contract if those surfaces exist
→ run prior-art gate for substantial new design
→ use reports/concept/ for design exploration/history when useful
→ establish design/ as the single current structured design authority when needed
→ establish CURRENT.md only when the project is long-running/multi-conversation or resume cost justifies it
→ expose workflow Skill only when a repeatable Agent workflow exists
→ project design/ into Skills/references
→ implementation/tests/evidence follow their owners
→ route local execution through DIRECT / LOCAL-QUICK / FORMAL as appropriate
```

Existing repositories upgrading from an earlier collaboration model use `migration.md` instead of replaying onboarding from scratch.

Do not create `reports/handoff/` merely because the project is long-running. Handoff appears only for real residual conversation-only continuity.

## Review criterion

A project architecture is sufficient when an unfamiliar Agent can determine:

```text
project authority
current work edge / next action when CURRENT is used
current design entry + topic ownership
design-history route when needed
existing-project migration route when applicable
real artifact owners
runtime/workflow entry
prior-art route for major redesign
exceptional conversation-only recovery route
mutable versus durable state
project tmp ownership
archive boundary
scientific-fact versus design authority
implementation/tooling authority
```

without reconstructing the previous conversation or reading unrelated manuals.
