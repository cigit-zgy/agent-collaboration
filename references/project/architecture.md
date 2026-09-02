# Project architecture and integration contract

This contract governs how a maintained scientific/software project joins `agent-collaboration` and how repository responsibilities are separated.

## Project entry

Root `AGENTS.md` is the project-local constitution. It identifies project identity, authority, repository ownership, workflow entry, runtime authority, and genuine human/trust checkpoints. Use `../collaboration/agents.md` plus `templates/agents.md` when authoring it.

A project workflow Skill may live at any project-declared path; it is not required to be repository-root `SKILL.md`.

## Canonical project architecture

Create only responsibilities that have a real owner, artifact, and consumer.

```text
<project>/
├── AGENTS.md
├── README.md
├── pyproject.toml               # conditional runtime authority
├── ARCHITECTURE.md              # conditional human architecture doc
├── <agent-name>/                # conditional Agent capability package
│   ├── SKILL.md
│   └── <capability>/SKILL.md
├── .agents/skills/              # conditional Codex discovery exposure
├── src/                         # conditional reusable implementation
├── models/                      # conditional durable model-specific artifacts
├── data/                        # conditional canonical reusable data
├── workspace/                   # conditional mutable working state
├── experiments/                 # conditional controlled investigations
├── tests/                       # conditional conformance/regression verification
├── docs/                        # conditional human technical docs
├── manuscript/                  # conditional publication assets
└── reports/
    ├── concept/
    ├── chatgpt/
    └── codex/
```

## Design and scientific authority

For maintained scientific projects that declare design authority:

```text
reports/concept/
= canonical User + ChatGPT accepted design

workflow/sub-Skills + references/
= operational projection

scripts/code/schemas
= implementation

tests/
= conformance verification

workspace/data/runtime artifacts
= produced or mutable state
```

Model-specific scientific facts remain grounded in the project's registered source/evidence chain rather than in the concept files. See `concept.md`.

## Reading modes

Routine:

```text
AGENTS.md
→ declared workflow SKILL.md
→ owning sub-Skill
→ required reference/script
```

Design/redesign/conformance:

```text
AGENTS.md
→ reports/concept/README.md
→ relevant governing concept
→ affected Skill/reference
→ implementation/tests as needed
```

## Ownership

- `AGENTS.md` — project constitution and routing.
- `README.md` — human orientation.
- `<agent-name>/` — project-owned Agent capabilities and operational projections.
- `src/` — reusable executable implementation/infrastructure.
- `models/` — durable model-specific definitions/artifacts.
- `data/` — canonical reusable project-owned datasets.
- `workspace/` — mutable operational state.
- `experiments/` — controlled reproducible investigations.
- `tests/` — conformance/regression verification.
- `docs/` — human technical documentation.
- `manuscript/` — publication assets.
- `reports/concept/` — accepted design when declared.
- `reports/chatgpt/` — committed local-execution specifications.
- `reports/codex/` — execution/verification evidence.

## Promotion

Experiment outputs become canonical `data/` or `models/` only after explicit project adoption with provenance. Exploratory code becomes reusable `src/` only when a real reusable consumer and stable contract exist. Live workspace state remains mutable even when captured as an experiment input/snapshot.

## Project onboarding

```text
inspect repository
→ establish project AGENTS.md
→ User + ChatGPT define accepted design in reports/concept/ when used
→ project Skills/references operationalize the design
→ implementation follows the projection
→ tests verify conformance
→ Codex is delegated only for genuinely local execution/verification
```

Project collaboration routes to `../collaboration/protocol.md` rather than duplicating global collaboration mechanics locally.
