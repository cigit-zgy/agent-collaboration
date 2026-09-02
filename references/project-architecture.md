# Canonical water research project architecture

This file is the current operational authority for repository architecture used by
maintained water-domain research projects under `agent-collaboration`.

## Canonical architecture

```text
<project>/
├── AGENTS.md
├── README.md
├── pyproject.toml               # conditional
├── ARCHITECTURE.md              # conditional
│
├── <agent-name>/                # conditional Agent/capability source
│   ├── SKILL.md
│   └── <capability>/SKILL.md
│
├── .agents/skills/              # conditional Codex discovery exposure
├── src/                         # conditional reusable implementation
├── models/                      # conditional durable model artifacts
├── data/                        # conditional canonical project data
├── workspace/                   # conditional mutable working state
├── experiments/                 # conditional controlled investigations
├── tests/                       # conditional conformance/regression verification
├── docs/                        # conditional technical documentation
├── manuscript/                  # conditional publication assets
│
└── reports/
    ├── concept/                 # accepted project solution/design only
    ├── chatgpt/                 # formal local-execution tasks
    └── codex/                   # execution evidence
```

Do not create optional directories merely to match the diagram. Create a responsibility
only when it has a real owner, artifact, and consumer.

## Design authority for water research projects

For maintained scientific/research projects:

```text
Level 1  reports/concept/
         canonical User + ChatGPT accepted solution/design

Level 2  workflow/sub-Skills + references/
         operational projection of that solution

Level 3  scripts / source code / schemas
         implementation

Level 4  tests/
         conformance verification

Level 5  workspace/data/runtime artifacts
         produced or mutable state
```

`reports/concept/` records the solution only. It does not record conversation history,
implementation progress, task history, test results, or runtime state.

Levels 2–5 must conform to Level 1. If an operational projection or implementation
disagrees with the governing concept, treat it as drift. Do not alter the concept to
match current code unless User + ChatGPT explicitly agree on a revised solution first.

Project design authority is distinct from scientific fact authority:

```text
project design truth
= reports/concept/

model/source scientific facts
= registered original source + evidence/provenance chain
```

Concepts define the system and scientific contracts; registered source evidence owns
model-specific values, equations, symbols, and claims.

## Reading modes

Routine execution:

```text
AGENTS.md
→ workflow SKILL.md
→ owning sub-Skill
→ required reference/script
```

Design, redesign, stage reconstruction, or conformance audit:

```text
AGENTS.md
→ reports/concept/README.md
→ relevant accepted design topic(s)
→ affected Skill/reference projection
→ implementation/tests as needed
```

## Project initialization

Bootstrap only assets with immediate responsibility:

```text
<project>/
├── AGENTS.md
├── README.md
└── reports/
    └── concept/
        └── README.md
```

Before downstream implementation is treated as authoritative, User + ChatGPT should
record the accepted project/stage solution in the relevant concept topic.

## Ownership contracts

### `AGENTS.md`

Project constitution and routing. It identifies the design authority, scientific source
authority, trust boundaries, repository ownership, collaboration source, workflow
entry, runtime authority, and human checkpoints. It does not duplicate stage manuals.

### `README.md`

Human-facing orientation only. It is not design or operational authority.

### `<agent-name>/`

Maintained source for a project-owned Agent capability system. `SKILL.md` routes the
workflow; sub-Skills own bounded capabilities. Skills/references project the accepted
concept design into executable Agent instructions and must not redefine it.

### `src/`

Reusable executable implementation/infrastructure: solvers, engines, parsers, APIs,
validators, and reusable utilities.

### `models/`

Durable model-specific definitions/artifacts. Boundary:

```text
reusable engine/algorithm/API → src/
model-specific durable object → models/
```

### `data/`

Canonical reusable project-owned datasets. Temporary run outputs do not become
canonical data automatically.

### `workspace/`

Mutable operational state for a model/case/task/Agent run. It is not the canonical
store for reusable datasets or formal experiment results.

### `experiments/`

Controlled reproducible investigations: calibration, simulation, benchmark,
validation, sensitivity/uncertainty, ablation, or case study. Investigation-specific
outputs remain experiment-owned until explicitly promoted.

### `tests/`

Verification that implementation/projections conform to accepted design and stable
contracts. Tests do not redefine design and do not substitute for scientific empirical
validation.

### `docs/`

Human-facing technical documentation beyond README. It is not design authority unless
a project explicitly declares otherwise.

### `manuscript/`

Publication assets. A manuscript consumes project outputs; it is not automatically a
source of truth for code/data/model objects.

### `reports/`

```text
reports/concept/  accepted project solution/design only
reports/chatgpt/  immutable committed execution specifications
reports/codex/    execution/verification evidence
```

## Promotion rules

- Experiment output becomes canonical `data/` only after explicit adoption with
  provenance.
- Experimental/calibrated artifacts become canonical `models/` only after explicit
  project adoption.
- Exploratory code becomes `src/` only after it has a real reusable consumer and
  stable contract.
- Workspace state may be captured as experiment input/snapshot; the live workspace
  remains mutable.

## Conditional creation triggers

Create only when the responsibility exists:

- `<agent-name>/`: repeatable Agent workflow exists;
- `.agents/skills/`: repo-scoped Codex auto-discovery is desired;
- `pyproject.toml`: project owns a Python runtime/tooling contract;
- `src/`: reusable implementation exists;
- `models/`: durable model-specific artifacts exist;
- `data/`: reusable canonical data exists;
- `workspace/`: mutable case/model/Agent state exists;
- `experiments/`: controlled research investigations exist;
- `tests/`: stable behavior/design conformity needs verification;
- `docs/`: durable technical explanation exceeds README/Skill scope;
- `manuscript/`: publication work is owned by the repository;
- `ARCHITECTURE.md`: cross-module structure is too complex to understand from
  AGENTS, concepts, workflow Skills, and ownership boundaries alone.

## Default rule

Preserve the direction of authority:

```text
User + ChatGPT agree on solution
→ reports/concept/ records that solution
→ Skills/references operationalize it
→ code/scripts implement it
→ tests verify it
→ runtime/workspace produces state
```
