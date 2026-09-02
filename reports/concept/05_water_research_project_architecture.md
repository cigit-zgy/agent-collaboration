---
id: 05
title: Canonical Water Research Project Architecture
status: active
created: 2026-09-02
updated: 2026-09-02
authority: global
scope: shared repository architecture for water mechanistic-model and water-domain Agent research projects
supersedes: null
related_tasks: []
---

# Canonical Water Research Project Architecture

## Current conclusion

Water-domain mechanistic-model projects and water-domain Agent projects use one
responsibility-based repository architecture rather than separate project templates.
The canonical responsibility map is documented in
`references/project-architecture.md`.

Root `AGENTS.md` is required as the maintained project constitution. An Agent workflow
package is conditional: when the project exposes a reusable Agent-operable workflow,
it uses a project-specific `<agent-name>/` directory whose root `SKILL.md` is the
composite/project workflow router and whose subdirectories contain bounded sub-Skills.
A literal `agent/` directory name is not required.

The standard responsibility slots are:

```text
<project>/
├── AGENTS.md                    required
├── README.md                    conditional
├── pyproject.toml               conditional
├── ARCHITECTURE.md              conditional
├── <agent-name>/                conditional Agent/Skill system
├── src/                         conditional reusable production code
├── models/                      conditional durable model definitions
├── data/                        conditional project-owned research data
├── workspace/                   conditional mutable case/model state
├── experiments/                 conditional controlled research investigations
├── tests/                       conditional verification
├── docs/                        conditional technical documentation
├── manuscript/                  conditional publication assets
└── reports/                     conditional collaboration/project knowledge
```

No optional directory is created merely to make a repository look complete.

`experiments/` is retained as the canonical container for controlled research
investigations, but it is not mandatory. It may contain calibration, simulation,
benchmark, validation, sensitivity/uncertainty, ablation, case-study, or other
scientifically controlled investigations. Experiment child names are chosen by the
science rather than prescribed globally. Experiments reference reusable code,
canonical data/models, and workspace/input authorities instead of duplicating those
responsibilities.

Mechanistic-model and Agent-centered projects therefore differ in which conditional
responsibilities they emphasize, not in their top-level architecture.

## Decision history

### 2026-09-02

#### Conclusion

One water-research project architecture is sufficient for both mechanistic/dynamic
model research and water-domain Agent research.

The architecture separates:

```text
project governance        → AGENTS.md
Agent-operable workflow   → <agent-name>/SKILL.md + sub-Skills, when needed
production implementation → src/
scientific model assets   → models/
research data             → data/
mutable working state     → workspace/
controlled investigations → experiments/
verification              → tests/
human technical docs      → docs/
publication               → manuscript/
collaboration knowledge   → reports/
```

Only root `AGENTS.md` is universally required by this maintained-project standard.
Other paths are conditional on a real project responsibility. Report subdirectories
are created when their first owned artifacts exist rather than as empty scaffolding.

A collection of coordinated Skills forms the Agent capability system. That system
may live under a project-specific `<agent-name>/` package, as in
`water-bioprocess-agent/`, with one composite workflow `SKILL.md` and bounded
sub-Skills. Embedded sub-Skills normally inherit root project `AGENTS.md`.

#### Rationale

A single responsibility map reduces unnecessary architectural variation between
closely related water research projects. Mechanistic modelling and Agent research
share the same underlying concerns—scientific assets, reusable implementation,
working state, controlled evaluation, verification, publication, and durable design
knowledge—even when the relative emphasis differs.

Making optionality explicit prevents empty-directory scaffolding and preserves the
same low-abstraction principle used for Skill packages. Retaining `experiments/` as a
well-defined conditional responsibility gives calibration, benchmark, validation,
and other research investigations a clear home without forcing fixed scientific
subcategories on every project.

#### Boundary

This concept defines repository responsibilities and creation conditions. It does not
prescribe the scientific method inside an experiment, force a Python runtime, require
all projects to expose an Agent workflow, or define project-specific model/data
schemas.

#### Impact

- `references/project-architecture.md`
- `references/project-agents-template.md`
- `references/project-skill-template.md`
- `references/project-integration.md`
- project onboarding in root `SKILL.md`
- future water-domain research repositories

#### Related tasks

None. User + ChatGPT settled the architecture and ChatGPT applied it directly through
connected repository tooling because no local-machine execution was required.
