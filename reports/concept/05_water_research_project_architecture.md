---
id: 05
title: Water research project architecture decisions
status: active
created: 2026-09-02
updated: 2026-09-02
role: decision_history
operational_authority:
  - references/project-architecture.md
  - references/project-integration.md
  - references/report-concept-policy.md
related_tasks: []
---

# Water research project architecture decisions

## Decision record

### 2026-09-02 — One responsibility-based architecture for water research

- Decision: mechanistic/dynamic-model projects and water-domain Agent projects share
  one repository vocabulary rather than separate project templates.
- Rationale: both project types need the same governance, implementation, model/data,
  working-state, controlled-investigation, validation, documentation, publication,
  and collaboration responsibilities; only the activated modules differ.
- Operational authority: `references/project-architecture.md`.

### 2026-09-02 — Keep `experiments/` as a conditional research responsibility

- Decision: `experiments/` is the standard container for controlled reproducible
  investigations such as calibration, simulation, benchmark, validation,
  sensitivity/uncertainty, ablation, and case studies, but is not created when no
  such responsibility exists.
- Rationale: preserve a clear home for research investigations without turning the
  architecture into a fixed directory checklist.
- Operational authority: `references/project-architecture.md`.

### 2026-09-02 — Explicit ownership and promotion between project responsibilities

- Decision: reusable executable infrastructure belongs in `src/`; durable
  model-specific definitions/artifacts belong in `models/`; canonical reusable data
  belongs in `data/`; mutable operational state belongs in `workspace/`; controlled
  research outputs remain experiment-owned until explicitly promoted.
- Rationale: prevent artifacts from drifting silently among code, model, data,
  workspace, and experiment responsibilities.
- Operational authority: `references/project-architecture.md`.

### 2026-09-02 — Minimal bootstrap, conditional expansion

- Decision: a new maintained water research project starts with `AGENTS.md`,
  human-facing `README.md`, and `reports/concept/README.md`; other responsibilities
  are created only when they have a real owner, artifact, and consumer.
- Rationale: initialize governance and the canonical project-design index without
  pre-creating empty code/data/experiment/Agent directories.
- Operational authority: `references/project-architecture.md`.

### 2026-09-02 — Water research concepts are the upstream project design source

- Decision: maintained water research projects use selected `reports/concept/*`
  topics as canonical User + ChatGPT design specifications for project-level
  scientific, architectural, trust, interface, and cross-stage decisions.
- Hierarchy: `concept design authority → Skill/reference operational projection →
  code/schema implementation → tests → runtime artifacts`.
- Rationale: the complete accepted project plan should remain independent of current
  implementation details, while Skills/references can stay compact and executable for
  Agents.
- Boundary: model-specific scientific facts still come from registered original
  sources and evidence/provenance, not from project design concepts.
- Runtime consequence: ordinary operation keeps the short
  `AGENTS → workflow Skill → sub-Skill → reference` route; design/redesign/audit reads
  only the relevant governing concept first.
- Operational authority: `references/project-architecture.md`,
  `references/project-integration.md`, `references/report-concept-policy.md`.
