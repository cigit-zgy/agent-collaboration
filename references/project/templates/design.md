# Project living-Design authoring template

Cold path: load only when creating/restructuring `reports/design/`.

Current-Design semantics are owned by `../design.md`; governance drift is owned by `../governance.md`.

## Directory shape

```text
reports/design/
├── README.md
├── 00_overview.md          # only when whole-system context is genuinely needed
├── 01_<topic>.md
├── 02_<topic>.md
└── ...
```

`reports/design/` is one mutable current set, not a history directory.

## README.md

Keep it navigational only:

```markdown
# Design map

`reports/design/` is the canonical current project Design.

| Order | design_id | File | Responsibility |
|---:|---|---|---|
| 00 | overview | `00_overview.md` | Whole-system architecture |
| 01 | <id> | `01_<topic>.md` | <one sentence> |
```

A bounded concern should route to one primary topic plus at most one necessary secondary topic. If one rule needs three or more current topics, restructure ownership before adding another topic.

## Topic file

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
## Accepted design
## Invariants / trust boundaries
## Ownership and interfaces
## Design acceptance
```

Remove empty sections rather than adding ceremony.

## One-owner check

Do not keep a current topic whose main role is to supersede, refine, override, or preserve another current topic for the same concern.

When responsibility changes:

```text
update/overwrite the real owner
→ merge/split/remove/reorder as needed
→ update README.md
→ remove superseded current files
```

Git preserves prior Design states. A new Concept preserves rationale only when the User explicitly requested Concept persistence.

## Content check

Reject content whose primary owner is:

```text
model/source-specific scientific fact
golden qualification or closure evidence
test/evaluation output
Codex task/report
current status/backlog
historical discussion
```

Keep only current project Design semantics with a real reusable owner.
