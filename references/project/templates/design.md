# Project living-design authoring template

Cold path: load this file only when creating/restructuring `reports/design/`.

Current-design semantics are owned by `../design.md`.

## Directory shape

```text
reports/design/
├── README.md
├── 00_overview.md          # only when whole-system context is needed
├── 01_<topic>.md
├── 02_<topic>.md
└── ...
```

The topic set is dynamic. `reports/design/` is not a chronological report family.

## README.md

Keep it navigational only:

```markdown
# Design map

`reports/design/` is the canonical current project design.
Historical reasoning lives in `reports/concept/`.

| Order | design_id | File | Responsibility |
|---:|---|---|---|
| 00 | overview | `00_overview.md` | Whole-system architecture |
| 01 | <id> | `01_<topic>.md` | <one sentence> |
```

Add short reading hints only when they reduce unrelated loading. Do not copy topic semantics into README.

## Topic file

Default shape:

```markdown
---
design_id: <stable-semantic-id>
title: <title>
status: active
role: design_authority
summary: >
  <one-sentence owned concern>
operational_projection:
  - <real downstream path when useful>
---

# <Title>

## Purpose
## Boundary
## Inputs / upstream state
## Accepted design
## Invariants / trust boundaries
## Lifecycle / transitions
## Ownership and interfaces
## Design acceptance
```

Remove empty sections rather than filling `N/A`.

## Restructuring checks

Create/split a topic only when it has an independent responsibility, stable semantics, distinct interface/state/trust/consumer/change lifecycle, and the split reduces unrelated context.

Merge topics when they always need to be read/changed together or duplicate semantics.

After accepted restructuring:

```text
update reports/design/README.md
→ keep only current topic files
→ remove superseded design files from reports/design/
→ renumber reading order when useful
→ preserve semantic identity through design_id
→ project accepted change into Skill/references before implementation
```

Reject living-design content whose primary purpose is historical reconstruction, including old copies, rejected alternatives, chronological decision narrative, progress logs, test history, or Codex execution detail. Those belong to Git history, `reports/concept/`, task/report owners, or another proper owner.
