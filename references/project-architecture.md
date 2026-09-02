# Canonical water research project architecture

This reference defines the default repository architecture for maintained water-domain
research projects under the `agent-collaboration` workflow. It is intended to cover
both mechanistic/dynamic-model projects and water-domain Agent projects with one
shared structure.

The architecture is responsibility-based rather than directory-count based. Only
project entry/governance assets are universal. All other directories are conditional
and are created only when the project has a real responsibility for them.

## Canonical architecture

```text
<project>/
├── AGENTS.md                    # required project constitution and maintenance entry
├── README.md                    # conditional human-facing project orientation
├── pyproject.toml               # conditional project runtime/tooling authority
├── ARCHITECTURE.md              # conditional human-facing system architecture
│
├── <agent-name>/                # conditional Agent capability package
│   ├── SKILL.md                 # Agent-facing composite/project workflow router
│   ├── <capability-a>/
│   │   └── SKILL.md
│   ├── <capability-b>/
│   │   └── SKILL.md
│   └── ...
│
├── src/                         # conditional reusable production implementation
├── models/                      # conditional durable model definitions/resources
├── data/                        # conditional project-owned research data
├── workspace/                   # conditional mutable case/model working state
├── experiments/                 # conditional controlled research investigations
├── tests/                       # conditional implementation/contract verification
├── docs/                        # conditional durable technical documentation
├── manuscript/                  # conditional publication/manuscript assets
│
└── reports/                     # collaboration/project knowledge when such assets exist
    ├── concept/                 # durable User + ChatGPT project conclusions
    ├── chatgpt/                 # implementation-ready ChatGPT task specifications
    └── codex/                   # Codex execution/verification evidence
```

Do not create empty optional directories merely to match this diagram. A repository
may legitimately contain only a subset of these responsibilities.

## Required versus conditional

| Path | Status | Responsibility |
|---|---|---|
| `AGENTS.md` | **REQUIRED** | Project constitution, authority, ownership boundaries, collaboration link, and routing to project knowledge/workflow. |
| `<agent-name>/SKILL.md` | **CONDITIONAL** | Required only when the project exposes an Agent-operable workflow/capability system. It is the workflow/router for that Agent package. |
| `reports/concept/` | **CONDITIONAL but standard for durable design** | Create when User + ChatGPT have durable project conclusions that should survive conversations. |
| `reports/chatgpt/` | **CONDITIONAL** | Create when a formal Codex task is issued. |
| `reports/codex/` | **CONDITIONAL** | Create when Codex execution evidence is produced. |
| All other paths | **CONDITIONAL** | Create only when the corresponding responsibility exists. |

Git does not preserve empty directories, so `reports/` subdirectories need not be
pre-created. Create them when the first owned artifact exists.

## `AGENTS.md` — required project entry

Root `AGENTS.md` is the repository-level constitution for Agents that develop,
maintain, or operate inside the project repository.

It should define only durable project-level concerns:

- project purpose and scope;
- scientific/product authority and trust boundaries;
- repository ownership boundaries;
- canonical collaboration reference;
- project concept/report locations;
- declared Agent workflow router, when one exists;
- runtime authority, when one exists;
- project-specific human checkpoints and hard invariants.

Do not turn `AGENTS.md` into a detailed scientific method, implementation manual, or
copy of the global collaboration protocol.

## `<agent-name>/` — conditional Agent capability system

Create one Agent capability package when the project has a reusable Agent-operable
workflow composed of one or more Skills.

Use an actual project-specific name such as `water-bioprocess-agent/`; do not require
a literal directory named `agent/`.

```text
<agent-name>/
├── SKILL.md
├── <capability-a>/SKILL.md
├── <capability-b>/SKILL.md
└── ...
```

The package root `SKILL.md` is the composite workflow/router. Sub-Skills own bounded
capabilities. A collection of coordinated Skills therefore forms the Agent capability
system, while the repository root `AGENTS.md` continues to govern the whole project.

Do not create a second repository-root `SKILL.md` merely for symmetry when the
project's actual workflow router is already `<agent-name>/SKILL.md`. The project
`AGENTS.md` must declare the canonical workflow-Skill path explicitly.

Embedded sub-Skills normally inherit the project root `AGENTS.md`; add nested
`AGENTS.md` only when a subtree has genuine additional maintenance rules.

## `src/` — conditional reusable production implementation

Create `src/` when the project owns reusable production code that should be separated
from research runs, workspaces, notebooks, or one-off analyses.

Examples include:

- reusable numerical/model infrastructure;
- parsers, APIs, libraries, or shared deterministic services;
- production utilities consumed by multiple project workflows.

Do not move code into `src/` merely because it is Python. A script owned by one Skill
may remain under that Skill's `scripts/` when that is its real consumer boundary.

## `models/` — conditional durable scientific model definitions

Create `models/` when the repository owns durable model definitions or model-level
resources independent of a single run/workspace.

Examples include:

- mechanistic model definitions;
- canonical parameter/model configurations;
- model schemas or reusable model resources;
- model fixtures intended to be retained as project assets.

Do not use `models/` for transient calibration outputs, one user's workspace state,
or generated artifacts that belong to a run.

## `data/` — conditional project-owned research data

Create `data/` only when research data are genuinely owned or managed by the
repository/project.

Typical contents may include stable raw/processed datasets, manifests, metadata, or
small fixtures. Large, sensitive, licensed, or externally governed datasets may live
outside Git; in that case keep only the project-approved manifests/metadata needed to
reproduce access and interpretation.

Do not use `data/` as a generic dumping directory for generated results or workspace
state.

## `workspace/` — conditional mutable working state

Create `workspace/` when workflows need model-specific, case-specific, or user/task
working state that evolves during operation.

Workspace content may include registered inputs, intermediate artifacts, retained
workflow state, generated evidence, candidate objects, or user-reviewed outputs as
defined by the project contract.

`workspace/` is not production source code and must not silently become the authority
for reusable implementation. Its lifecycle and immutability rules are project-specific
and belong in `AGENTS.md`, concepts, and the owning workflow Skill.

## `experiments/` — conditional controlled research investigations

Create `experiments/` when the project performs controlled scientific investigations
whose design, execution, and outputs need to be preserved as research evidence.

This directory is intentionally broad enough to cover water-domain work such as:

- calibration and parameter-estimation studies;
- simulation studies;
- benchmark and baseline comparisons;
- validation studies;
- sensitivity/uncertainty analysis;
- ablation studies;
- case studies or controlled method comparisons.

`experiments/` is **not mandatory**. Create it only when the project has such
research investigations.

Each experiment should make its scientific intent and reproducibility boundary clear.
As appropriate, preserve or point to:

```text
question / hypothesis
configuration / protocol
input-data or model references
implementation/version reference
outputs/results
analysis or evaluation summary
```

The exact subdirectory names are chosen by the science. Do not force every project to
use fixed `calibration/`, `benchmark/`, `ablation/`, or other child directories.

Do not put reusable production code, canonical project datasets, or mutable workflow
state into `experiments/` merely because they were used by an experiment. Experiments
reference those authorities instead.

## `tests/` — conditional verification

Create root `tests/` when the project owns implementation or cross-component contracts
that warrant repository-level verification.

Typical responsibilities include:

- production-code behavior;
- cross-Skill integration contracts;
- model/schema invariants;
- stable artifact shapes;
- project-level regression tests.

Skill-local executable behavior may instead be tested inside the owning Skill package
when that boundary is clearer. Do not duplicate the same contract at both levels.

## `docs/` — conditional durable technical documentation

Create `docs/` for durable human-facing technical or design documentation that is too
large or specialized for `README.md`/`AGENTS.md` and is not a collaboration concept.

Examples include user/developer guides, architecture explanations, generated
reference documentation, or long technical specifications intended for human
consumption.

Do not use `docs/` as a replacement for `reports/concept/`: accepted User + ChatGPT
design truth belongs in concepts; general human documentation belongs in `docs/`.

## `manuscript/` — conditional publication assets

Create `manuscript/` when the repository owns a paper, preprint, supplement, figure
source, response-to-reviewers material, or other publication artifacts.

Keep manuscript assets separate from production code, datasets, and transient
workspace state. Scientific claims in the manuscript do not automatically become
software/model authority unless the project explicitly promotes them into the
relevant contract or concept.

## `README.md` — conditional human-facing orientation

Create root `README.md` when humans need a conventional repository landing page for
purpose, setup, usage, contribution, publication, or release information.

It is strongly recommended for shared or open-source repositories, but it is not an
Agent runtime requirement and should not duplicate the detailed workflow in
`SKILL.md` or project governance in `AGENTS.md`.

## `pyproject.toml` — conditional Python runtime/tooling authority

Create root `pyproject.toml` only when the project owns a Python package/runtime or
project-wide Python tooling contract.

If executable code belongs entirely to an independently maintained Skill or another
runtime authority, do not create a project `pyproject.toml` merely for symmetry.
Environment ownership and rebuild policy follow `skill-environment-policy.md` plus
project-specific rules.

## `ARCHITECTURE.md` — conditional human-facing system map

Create `ARCHITECTURE.md` only when the project has cross-module/system structure that
cannot be explained compactly through `AGENTS.md`, the workflow Skill, and concept
routing.

It may describe stable component boundaries and data/control flow for human
maintainers, but it must not become a second source of truth for contracts already
owned by project concepts or Skills.

## `reports/` — conditional collaboration/project knowledge

Use the standard ownership split when collaboration artifacts exist:

```text
reports/concept/   durable User + ChatGPT conclusions
reports/chatgpt/   committed implementation-ready Codex tasks
reports/codex/     Codex execution and verification evidence
```

Do not put ordinary experiment results, user workspace output, or manuscript drafts
into these directories.

## Mechanistic-model and Agent projects use the same architecture

The structure is deliberately shared.

A mechanistic/dynamic-model project may emphasize:

```text
models/
data/
experiments/
src/
tests/
```

An Agent-centered water project may emphasize:

```text
<agent-name>/
workspace/
experiments/
src/
tests/
```

These are different responsibility mixes, not different project architectures.

## Initialization rule

Initialize in this order:

```text
1. Create/normalize root AGENTS.md.
2. Identify the project's real responsibility boundaries.
3. Create only directories with current real consumers.
4. If the project exposes an Agent workflow, choose <agent-name>/ and create its
   SKILL.md from project-skill-template.md.
5. Add sub-Skills only for bounded reusable capabilities.
6. Add runtime, models, data, workspace, experiments, tests, docs, or manuscript
   directories only when their responsibilities actually exist.
7. Create report directories when the first owned collaboration asset is written.
```

The template is a responsibility map, not a command to scaffold every possible
folder.