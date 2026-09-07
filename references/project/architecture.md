# Project architecture and integration contract

Load this reference for project repository ownership, authority surfaces, runtime reading routes, onboarding, and responsibility placement.

Report-family/archive layout is owned by `reports.md`. External CLI/API/schema integration is owned by `external-tools.md`. Detailed local Git/worktree/tmp execution is owned by `../collaboration/execution.md`.

## Project entry

Root `AGENTS.md` is the project-local constitution. It identifies project identity, authority, ownership boundaries, workflow entry, runtime/tooling authority, context-recovery route when used, and genuine human/trust checkpoints.

Use `../collaboration/agents.md` plus `templates/agents.md` when authoring it.

A project workflow Skill may live at any project-declared path; it is not required to be repository-root `SKILL.md`.

## Responsibility-based architecture

There is no universal canonical project filesystem beyond collaboration-wide hard contracts such as the project `reports/` and root `00_archive/` rules in `reports.md`.

Create only responsibilities with a real owner, artifact, and consumer. Common patterns include:

| Responsibility | Common path | Meaning |
|---|---|---|
| project constitution | `AGENTS.md` | repository-scoped authority and routing |
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
| accepted project design | `reports/concept/` | canonical design only when declared |
| formal delegated tasks | `reports/chatgpt/` | committed FORMAL specifications |
| Codex execution evidence | `reports/codex/` | FORMAL execution/verification reports |
| conversation continuity | `reports/handoff/` | context-recovery snapshots; never design/task authority |
| historical retention | `00_archive/` | single repository-root history boundary; never active authority |
| Agent-local temporary state | `tmp/` | project-owned ephemeral boundary |

If `reports/` exists, its only allowed direct children, filename contract, common metadata envelope, handoff placement, and archive rules are defined by `reports.md` and are not project-optional variants.

## Design authority

When a scientific project declares `reports/concept/` as canonical design authority, `concept.md` owns writing, review, adjudication, freeze, reopen, and projection lifecycle.

Before a new project, core subsystem, major algorithm/architecture, or comparable gate-triggered design is frozen, complete `prior-art.md`.

```text
external prior art
= design evidence

accepted project concept
= design authority

registered source/evidence
= model-specific scientific fact authority
```

Conversation handoffs are context-recovery artifacts only. They may summarize accepted decisions and repository state, but they never supersede current `AGENTS.md`, concept, committed task, registered scientific source/evidence, or repository state.

## Runtime reading routes

Expose the shortest stable route for routine operation:

```text
AGENTS.md
→ declared workflow SKILL.md
→ owning sub-Skill/reference/script
```

Do not force ordinary execution through project design/history files when the operational projection is already stable.

### New project / major design

```text
AGENTS.md
→ current agent-collaboration prior-art route
→ strongest relevant external precedents
→ relevant reports/concept artifact(s)
→ operational projection
```

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
reusable engine/algorithm/API → reusable implementation owner
model-specific durable object → model-artifact owner
canonical reusable dataset    → data owner
mutable current run state      → workspace owner
controlled investigation      → experiment owner
conversation continuity       → handoff owner
historical retained state     → root 00_archive owner
Agent-created ephemeral state → project tmp boundary + collaboration execution owner
```

Promotion between responsibilities is explicit. Experiment outputs become canonical data/model artifacts only after project adoption with provenance. Exploratory code becomes reusable implementation only when a real reusable consumer and stable contract exist. Live workspace state remains mutable. Handoff summaries do not promote themselves into concept/task/source authority merely because they are committed.

## Project-local ephemeral boundary

`tmp/` is the canonical project-owned location for Agent-created local ephemeral state. Detailed placement, `WORK_ID`, linked-worktree, cleanup, and Git-safety semantics are owned by `../collaboration/execution.md`.

## Project onboarding

```text
inspect actual repository
→ establish concise project AGENTS.md
→ declare real ownership + runtime/tooling boundaries
→ apply reports/archive hard contract if those surfaces exist
→ run prior-art gate for substantial new design
→ inspect strongest paper-linked/mature open-source precedents
→ define/accept project concept when needed
→ expose workflow Skill only when a repeatable Agent workflow exists
→ project Skills/references operationalize accepted design
→ implementation follows collaboration implementation contract + project tooling
→ tests/evidence verify conformance
→ route local execution through DIRECT / LOCAL-QUICK / FORMAL as appropriate
```

Conversation handoff support is added only on first real context migration by creating the first canonically named file under `reports/handoff/`; no separate root `handoff/` or handoff `README.md` is created.

## Review criterion

A project architecture is sufficient when an unfamiliar Agent can determine:

```text
project authority
real artifact owners
runtime/workflow entry
prior-art/design route when needed
context-recovery route when handoffs exist
mutable versus durable state
project tmp ownership
archive boundary
scientific-fact versus design authority
implementation/tooling authority
```

without inferring an undocumented filesystem contract or reading unrelated collaboration manuals.
