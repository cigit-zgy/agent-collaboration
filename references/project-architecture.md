# Canonical water research project architecture

This file is the current operational authority for repository architecture used by
maintained water-domain research projects under `agent-collaboration`. One structure
covers mechanistic/dynamic-model research and water-domain Agent research.

The architecture is responsibility-based. Do not create directories merely because
they appear in the canonical diagram.

## Canonical architecture

```text
<project>/
├── AGENTS.md                    # required project constitution
├── README.md                    # normal human-facing project orientation
├── pyproject.toml               # conditional project runtime/tooling authority
├── ARCHITECTURE.md              # conditional cross-module system explanation
│
├── <agent-name>/                # conditional maintained Agent/capability source
│   ├── SKILL.md                 # composite/project workflow Skill
│   └── <capability>/SKILL.md    # conditional sub-Skills
│
├── .agents/skills/              # conditional Codex repo-scoped discovery exposure
├── src/                         # conditional reusable production implementation
├── models/                      # conditional durable model definitions/resources
├── data/                        # conditional canonical project-owned research data
├── workspace/                   # conditional mutable case/model working state
├── experiments/                 # conditional controlled research investigations
├── tests/                       # conditional implementation/contract verification
├── docs/                        # conditional durable technical documentation
├── manuscript/                  # conditional publication assets
│
└── reports/
    ├── concept/                 # decision history/rationale when needed
    ├── chatgpt/                 # formal Codex tasks when issued
    └── codex/                   # Codex execution evidence when produced
```

`.agents/skills/` is a Codex discovery surface, not a second maintained source tree.
When a project Skill is maintained elsewhere in the repository, prefer a stable
repo-local symlink rather than a duplicate copy if auto-discovery is desired.

## Project initialization

For a new maintained water research project, bootstrap only assets with immediate
responsibility:

```text
<project>/
├── AGENTS.md
├── README.md
└── reports/
    └── concept/
        └── README.md
```

These files establish project governance, human orientation, and an index location
for durable design history. Do not pre-create empty `chatgpt/`, `codex/`, `src/`,
`models/`, `data/`, `workspace/`, `experiments/`, `tests/`, `docs/`, `manuscript/`,
`<agent-name>/`, `.agents/skills/`, `pyproject.toml`, or `ARCHITECTURE.md`.

Expand only when a real owner, artifact, and consumer exist.

## Ownership contracts

### `AGENTS.md`

Required repository constitution for Agent maintenance/operation. It defines project
purpose, authority/trust boundaries, repository ownership, collaboration link,
workflow entry when present, runtime authority when present, human checkpoints, and
hard invariants.

It does not contain detailed workflow algorithms or duplicate global collaboration
policy.

### `README.md`

Human-facing project orientation: purpose, status, setup pointers, and navigation.
It is not an Agent operational authority.

### `<agent-name>/`

Maintained source for a project-owned Agent capability system. Use when the project
exposes a repeatable Agent-operable workflow.

`<agent-name>/SKILL.md` is the composite/project workflow router. Sub-Skills own
bounded capabilities. Do not create one `AGENTS.md` per sub-Skill unless genuine
local maintenance rules differ from the project root.

If Codex auto-discovery is desired, expose the package under
`$REPO_ROOT/.agents/skills/` according to `skill-repository-policy.md`.

### `src/`

Reusable executable implementation and infrastructure. Examples: solvers, model
engines, parsers, APIs, validators, reusable utilities.

`src/` owns executable behavior; it does not own model-specific scientific content
merely because code can represent it.

### `models/`

Durable model-specific definitions/resources that are treated as project research
objects rather than general implementation infrastructure: equations/specifications,
parameter sets, schemas/configurations, calibrated model artifacts, or canonical
model packages.

Boundary with `src/`:

```text
reusable engine/algorithm/API implementation → src/
model-specific durable definition/artifact    → models/
```

A model implemented as Python may have reusable execution code in `src/` and
model-specific definitions/configuration under `models/`; do not duplicate the same
truth in both.

### `data/`

Canonical project-owned datasets intended for reuse across analyses/experiments.
Raw/processed naming is project-specific; provenance and licensing/size constraints
must be defined when data is actually introduced.

Temporary run outputs do not become canonical `data/` automatically.

### `workspace/`

Mutable operational state for a particular model, case, user task, or Agent run.
Examples: source bundles, prepared evidence, working candidates, intermediate review
state, temporary generated artifacts.

`workspace/` is not the canonical store for reusable datasets or formal experiment
results.

### `experiments/`

Controlled research investigations with reproducible purpose and boundaries. It may
contain calibration studies, simulations, benchmarks, validation studies,
sensitivity/uncertainty analyses, ablations, or case studies.

Each experiment owns its investigation-specific configuration, inputs/references,
outputs, and analysis products unless something is deliberately promoted to another
project-level authority.

### `tests/`

Regression/contract verification for reusable code, schemas, APIs, deterministic
workflows, or other stable behavior. Do not use tests as a substitute for scientific
experiments or empirical validation.

### `docs/`

Durable human-facing technical documentation that is too detailed for README and is
not an Agent runtime contract. Do not use it as a second operational policy layer.

### `manuscript/`

Paper source, figures/tables assembled for publication, supplementary material, and
submission assets. The manuscript may consume project outputs but does not become
the source of truth for production code/data/model objects unless explicitly defined.

### `reports/`

Collaboration assets only:

```text
reports/concept/  accepted decision history/rationale + pointers to current authority
reports/chatgpt/  immutable committed local-execution tasks
reports/codex/    execution/verification evidence
```

Current operational policy belongs in the project's owning contracts/Skills, not in
concept history.

## Promotion rules between responsibilities

Do not allow artifacts to drift silently between directories.

### Experiment → canonical data

An experiment-generated dataset moves/becomes canonical under `data/` only after an
explicit project decision that it is reusable outside that experiment, with enough
provenance to identify its origin and transformation. Until then it remains an
experiment output.

### Experiment → model

An experimental calibration/model artifact becomes a durable `models/` artifact only
when the project explicitly adopts it as a reusable model definition/state. Until
then it remains experiment-owned.

### Exploratory implementation → `src/`

Code written inside an experiment/workspace becomes `src/` only when it has a real
reusable consumer and a stable implementation contract. Do not promote exploratory
code merely to make the repository look clean.

### Workspace → experiment

A workspace artifact may be captured as an experiment input/snapshot when the
experiment requires it. The experiment owns the captured research input; the live
workspace remains mutable and must not be treated as immutable experiment evidence.

## Conditional creation triggers

Create only when the responsibility exists:

- `<agent-name>/`: repeatable Agent-operable workflow exists;
- `.agents/skills/`: Codex repo-scoped auto-discovery is desired;
- `pyproject.toml`: project owns a Python runtime/tooling contract;
- `src/`: reusable production implementation exists;
- `models/`: model-specific durable artifacts exist;
- `data/`: reusable canonical project data exists;
- `workspace/`: mutable model/case/Agent working state exists;
- `experiments/`: controlled reproducible research investigations exist;
- `tests/`: stable behavior needs regression protection;
- `docs/`: durable technical explanation exceeds README/Skill scope;
- `manuscript/`: publication work is owned by the repository;
- `ARCHITECTURE.md`: cross-module structure is too complex to understand from
  `AGENTS.md`, workflow Skill, and directory ownership alone.

## Default rule

The template is a vocabulary of responsibilities, not a directory checklist.
Initialize the smallest meaningful project and grow it only when a responsibility is
real.
