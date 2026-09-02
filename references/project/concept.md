# Project concept and report policy

This contract governs formal collaboration reports and `reports/concept/` for maintained scientific/research projects.

## Stable report layout

```text
reports/
├── concept/   current accepted project design
├── chatgpt/   committed local-execution specifications
└── codex/     execution and verification evidence
```

Formal task/report paths remain stable after issue.

## Concept responsibility

When a project declares `reports/concept/` as design authority, each concept topic contains only the current User + ChatGPT accepted solution for its concern. Appropriate content includes project purpose, architecture/stage boundaries, scientific representation design, interfaces/ownership, trust/lifecycle, provenance/evidence, validation/promotion, human review, and project-specific testing/release design.

Implementation history, task execution evidence, test logs, transient filesystem state, and model-specific scientific values belong to their own authorities rather than the concept.

## Authority chain

```text
reports/concept/
→ SKILL.md + references/
→ scripts/code/schemas
→ tests/
→ runtime artifacts
```

If downstream projection or implementation differs from the governing concept, treat it as drift. A design change begins with an explicit User + ChatGPT decision and concept update, then propagates downstream.

Scientific fact authority remains separate:

```text
project design truth = reports/concept/
model scientific facts = registered source + evidence/provenance
```

## Concept index

`reports/concept/README.md` maps active design topics to their operational projections. It is a design map rather than an implementation-status board.

A topic may use minimal metadata:

```yaml
---
id: <ID>
title: <TITLE>
status: active
role: design_authority
operational_projection:
  - <path>
---
```

## Reading paths

Routine execution can use the already-derived operational projection. Design/redesign/conformance work begins from the relevant governing concept before modifying Skills/references/code/tests.

## Collaboration-repository exception

`agent-collaboration` itself is a protocol/Skill repository; its active policy lives in `references/` and its existing `reports/concept/` files are decision history/rationale.

Task/report metadata formats live in `../collaboration/templates/chatgpt-task.md` and `../collaboration/templates/codex-report.md`.
