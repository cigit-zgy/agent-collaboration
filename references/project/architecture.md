# Project architecture and integration contract

Load this reference for project repository ownership, authority surfaces, runtime reading routes, onboarding, and responsibility placement.

Existing-project migration to current collaboration policy is owned by `migration.md`. Report-family/archive layout is owned by `reports.md`. Concept-journal semantics are owned by `concept.md`. Current living-design structure is owned by `design.md`. External CLI/API/schema integration is owned by `external-tools.md`. Detailed local Git/worktree/tmp execution is owned by `../collaboration/execution.md`.

## Project entry

Root `AGENTS.md` is the project-local constitution. It identifies project identity, authority, ownership boundaries, workflow entry, runtime/tooling authority, context-recovery route when used, and genuine human/trust checkpoints.

Use `../collaboration/agents.md` plus `templates/agents.md` when authoring it.

A project workflow Skill may live at any project-declared path; it is not required to be repository-root `SKILL.md`.

## Responsibility-based architecture

There is no universal canonical project filesystem beyond collaboration-wide hard contracts such as the project `reports/`, `design/` authority semantics when used, and root `00_archive/` rules.

Create only responsibilities with a real owner, artifact, and consumer. Common patterns include:

| Responsibility | Common path | Meaning |
|---|---|---|
| project constitution | `AGENTS.md` | repository-scoped authority and routing |
| current accepted design | `design/` | canonical living design; one current set only |
| design exploration/history | `reports/concept/` | chronological concept journal; non-authoritative |
| human orientation | `README.md` | human-facing introduction/quick start |
| runtime/tooling authority | `pyproject.toml` or equivalent | dependencies, mechanical style, tooling |
| Agent capability package | `<agent-name>/` | project-owned workflow/sub-Skills when present |
| reusable implementation | `src/` | reusable executable code/infrastructure |
| durable model artifacts | `models/` | project-adopted model-specific artifacts |
| canonical reusable data | `data/` | project-adopted datasets |
| mutable work state | `workspace/` | current case/model/Agent operational state |
| controlled investigations | `experiments/` | reproducible calibration/simulation/benchmark/case-study work |
| conformance/regression checks | `tests/` | tests for stable contracts/implementation |
| human technical documentation | `docs/` | durable explanation beyond README |
| publication assets | `manuscript/` | manuscript/figure/supplement materials when owned here |
| formal delegated tasks | `reports/chatgpt/` | committed FORMAL specifications |
| Codex execution evidence | `reports/codex/` | FORMAL execution/verification reports |
| conversation continuity | `reports/handoff/` | context-recovery snapshots; never design/task authority |
| historical retention | `00_archive/` | single repository-root history boundary; never active authority |
| Agent-local temporary state | `tmp/` | project-owned ephemeral boundary |

If `reports/` exists, its only allowed direct children, filename contract, common metadata envelope, handoff placement, and archive rules are defined by `reports.md`.

## Design authority

For projects that maintain explicit architecture/design, canonical current design lives in:

```text
design/
```

`design.md` owns dynamic topic decomposition, current-only semantics, filename/identity rules, and projection order.

The authority relationship is:

```text
reports/concept/
= historical/exploratory design input

design/
= current accepted project design authority

registered source/evidence
= model-specific scientific fact authority
```

Before a new project, core subsystem, major algorithm/architecture, or comparable gate-triggered design is accepted into `design/`, complete `prior-art.md`.

Conversation handoffs are context-recovery artifacts only. They may summarize accepted decisions and repository state, but they never supersede current `AGENTS.md`, `design/`, committed task, registered scientific source/evidence, or repository state.

## Runtime reading routes

Expose the shortest stable route for routine operation:

```text
AGENTS.md
→ declared workflow SKILL.md
→ owning sub-Skill/reference/script
```

Do not force ordinary execution through project design/history files when the operational projection is already stable.

### Existing-project migration

When a repository must be migrated to a newer collaboration model:

```text
current collaboration SKILL.md
→ migration.md
→ target project AGENTS.md + current branch/HEAD/state
→ design/README.md when present
→ only directly relevant current design/history/task/report anchors
→ migrate only drifted surfaces
```

Do not start by rereading the old conversation, all concept notes, all reports, or the complete collaboration reference tree. If another conversation is taking over, the old conversation supplies only the compact bootstrap defined by `templates/migration-bootstrap.md`.

Project-policy migration does not require a conversation handoff unless meaningful non-repository continuity would otherwise be lost.

### Current design / conformance

```text
AGENTS.md
→ design/README.md
→ directly relevant current design topic(s)
→ affected Skill/reference projection
→ implementation/tests as needed
```

Do not preload all design topics for a bounded concern.

### New project / major design

```text
AGENTS.md
→ current agent-collaboration prior-art route
→ strongest relevant external precedents
→ one or more reports/concept notes as working record
→ User + ChatGPT adjudication
→ design/ current-state update
→ operational projection
```

### Historical design rationale

```text
current design topic
→ only relevant reports/concept note(s) when needed
```

Do not use concept history as the normal route to discover current design.

### Conversation/context recovery

When `reports/handoff/` exists:

```text
AGENTS.md
→ newest valid reports/handoff/YYMMDD_handoff_NN.md
→ re-resolve current collaboration/project authority
→ inspect current repository state
→ continue through normal workflow/design route
```

Do not read every historical handoff by default.

### External tool integration

When the active concern is an evolving external CLI/API/schema/parser/simulator interface, route directly from collaboration `SKILL.md` to `external-tools.md`.

## Ownership boundaries

Use responsibilities rather than folder symmetry:

```text
current project design          → design/ owner
design exploration/history      → reports/concept owner
reusable engine/algorithm/API    → reusable implementation owner
model-specific durable object   → model-artifact owner
canonical reusable dataset      → data owner
mutable current run state       → workspace owner
controlled investigation        → experiment owner
conversation continuity         → handoff owner
historical retained state       → root 00_archive owner
Agent-created ephemeral state   → project tmp boundary + collaboration execution owner
```

Promotion between responsibilities is explicit. Concept notes become design only through User + ChatGPT adjudication and a concrete update of `design/`. Experiment outputs become canonical data/model artifacts only after project adoption with provenance. Exploratory code becomes reusable implementation only when a real reusable consumer and stable contract exist.

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
→ establish design/ as the single current structured design authority
→ expose workflow Skill only when a repeatable Agent workflow exists
→ project design/ into Skills/references
→ implementation follows collaboration implementation contract + project tooling
→ tests/evidence verify design/ and implementation conformance
→ route local execution through DIRECT / LOCAL-QUICK / FORMAL as appropriate
```

This onboarding route is for establishing a project model. Existing repositories upgrading from an earlier collaboration model use `migration.md` instead of replaying onboarding from scratch.

Conversation handoff support is added only on first real context migration by creating the first canonically named file under `reports/handoff/`; no separate root `handoff/` or handoff `README.md` is created.

## Review criterion

A project architecture is sufficient when an unfamiliar Agent can determine:

```text
project authority
current design entry + topic ownership
design-history route when needed
existing-project migration route when applicable
real artifact owners
runtime/workflow entry
prior-art route for major redesign
context-recovery route when handoffs exist
mutable versus durable state
project tmp ownership
archive boundary
scientific-fact versus design authority
implementation/tooling authority
```

without inferring an undocumented filesystem contract or reading unrelated collaboration manuals.
