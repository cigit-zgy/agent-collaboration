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
    ├── concept/                 # canonical project design specifications + decision history
    ├── chatgpt/                 # formal Codex tasks when issued
    └── codex/                   # Codex execution evidence when produced
```

`.agents/skills/` is a Codex discovery surface, not a second maintained source tree.
When a project Skill is maintained elsewhere in the repository, prefer a stable
repo-local symlink rather than a duplicate copy if auto-discovery is desired.

## Design-authority model for water research projects

Maintained water research projects under this architecture use selected
`reports/concept/` topics as the canonical User + ChatGPT design specification for
project-level scientific, architectural, trust, interface, and cross-stage decisions.
Root `AGENTS.md` and the concept index declare the exact governed topics.

Use the following hierarchy:

```text
Level 1  reports/concept/
         canonical design specification: WHAT + WHY

Level 2  workflow/sub-Skills + references/
         operational projection of the accepted design

Level 3  scripts / source code / schemas
         implementation

Level 4  tests/
         conformance verification

Level 5  workspace/data/runtime artifacts
         produced or mutable project state
```

Levels 2–5 must conform to Level 1. If an operational projection or implementation
disagrees with the governing concept, treat it as drift unless User + ChatGPT
explicitly approve and update the design first.

This does not make concepts the authority for model-specific scientific facts.
Registered original sources and the project's evidence/provenance chain remain the
authority for source-grounded scientific values, equations, symbols, and claims.

Concepts therefore answer “what system are we building and why”; source evidence
answers “what does this scientific model/source actually state.”

## Runtime versus design reading

Routine Agent operation should not load the full concept corpus:

```text
AGENTS.md
→ workflow SKILL.md
→ owning sub-Skill
→ required reference/script
```

Design/redesign/conformance audit uses:

```text
AGENTS.md
→ reports/concept/README.md
→ relevant design-authority topic(s)
→ affected Skill/reference projection
→ implementation/tests as needed
```

This preserves progressive disclosure while keeping the User + ChatGPT design as the
single design truth.

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

These files establish project governance, human orientation, and the index for
canonical design topics. Do not pre-create empty `chatgpt/`, `codex/`, `src/`,
`models/`, `data/`, `workspace/`, `experiments/`, `tests/`, `docs/`, `manuscript/`,
`<agent-name>/`, `.agents/skills/`, `pyproject.toml`, or `ARCHITECTURE.md`.

Expand only when a real owner, artifact, and consumer exist. Record a mature
scientific/architectural design in the appropriate concept topic before downstream
Skills/references/code are treated as its implementation.

## Ownership contracts

### `AGENTS.md`

Required repository constitution for Agent maintenance/operation. It defines project
purpose, design-authority declaration, scientific evidence authority/trust boundaries,
repository ownership, collaboration link, workflow entry when present, runtime
authority when present, human checkpoints, and hard invariants.

It does not contain detailed workflow algorithms or duplicate global collaboration
policy.

### `README.md`

Human-facing project orientation: purpose, status, setup pointers, and navigation.
It is not an Agent operational or scientific authority.

### `<agent-name>/`

Maintained source for a project-owned Agent capability system. Use when the project
exposes a repeatable Agent-operable workflow.

`<agent-name>/SKILL.md` is the composite/project workflow router. Sub-Skills own
bounded capabilities. In design-authoritative projects, Skills/references are
operational projections of the governing concept design and must not redefine it.

Do not create one `AGENTS.md` per sub-Skill unless genuine local maintenance rules
differ from the project root.

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
results. In source-grounded modelling projects, registered original source bytes and
their evidence/provenance chain may form a scientific fact authority inside the
workspace; this remains distinct from project design authority in `reports/concept/`.

### `experiments/`

Controlled research investigations with reproducible purpose and boundaries. It may
contain calibration studies, simulations, benchmarks, validation studies,
sensitivity/uncertainty analyses, ablations, or case studies.

Each experiment owns its investigation-specific configuration, inputs/references,
outputs, and analysis products unless something is deliberately promoted to another
project-level authority.

### `tests/`

Regression/contract verification for reusable code, schemas, APIs, deterministic
workflows, or other stable behavior. Tests demonstrate conformance to accepted design
and operational contracts; they do not gain authority to redefine those contracts.
Do not use tests as a substitute for scientific experiments or empirical validation.

### `docs/`

Durable human-facing technical documentation that is too detailed for README and is
not an Agent runtime or design authority unless the project explicitly declares a
specific document otherwise.

### `manuscript/`

Paper source, figures/tables assembled for publication, supplementary material, and
submission assets. The manuscript may consume project outputs but does not become
the source of truth for production code/data/model objects unless explicitly defined.

### `reports/`

Collaboration and design assets:

```text
reports/concept/  canonical User + ChatGPT project design specifications and their decision history
reports/chatgpt/  immutable committed local-execution tasks
reports/codex/    execution/verification evidence
```

Concept design authority governs project scientific/architectural design. Operational
execution is projected into Skills/references. Model-specific scientific facts remain
grounded in registered source evidence rather than project concepts.

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
  `AGENTS.md`, governing concepts, workflow Skill, and directory ownership alone.

## Default rule

The template is a vocabulary of responsibilities, not a directory checklist.
Initialize the smallest meaningful project and grow it only when a responsibility is
real. Preserve the direction of authority:

```text
User + ChatGPT design
→ concept design authority
→ operational projection
→ implementation
→ verification
→ runtime artifacts
```
