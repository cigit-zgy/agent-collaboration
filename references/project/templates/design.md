# Project living-design authoring template

Cold path: load this file only when creating a new `design/` tree, adding/splitting/merging a design topic, or materially rewriting living-design structure.

Current-design semantics and dynamic decomposition rules are owned by `../design.md`.

## Recommended directory shape

```text
design/
├── README.md
├── 00_overview.md          # when whole-system context is needed
├── 01_<topic>.md
├── 02_<topic>.md
└── ...
```

The numbered topic set is dynamic. Do not create placeholder files for a predetermined architecture.

## README.md

Keep it short and navigational:

```markdown
# Design map

`design/` is the canonical current project design. Historical reasoning lives in `reports/concept/`.

| Order | design_id | File | Responsibility |
|---:|---|---|---|
| 00 | overview | `00_overview.md` | Whole-system architecture |
| 01 | <id> | `01_<topic>.md` | <one sentence> |
| 02 | <id> | `02_<topic>.md` | <one sentence> |
```

Add a short reading hint only when it materially reduces unnecessary loading, for example:

```text
For source registration → read 01_source_registration.md only.
For whole pipeline redesign → read 00_overview.md + affected topic files.
```

Do not copy topic semantics into README.

## 00_overview.md

Use only when the project has multiple interacting design concerns or a whole-system topology that cannot be recovered from the map alone.

Suggested information:

```markdown
---
design_id: overview
title: Project design overview
status: active
role: design_authority
summary: >
  <whole-system responsibility>
---

# Project design overview

## Purpose
## Whole-system architecture
## Major domains / stages
## Cross-topic boundaries
## Topic relationships
## Whole-design acceptance
```

Do not restate each topic's detailed contract.

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
<Why this current concern exists.>

## Boundary
<What it owns; adjacent ownership only where ambiguity is plausible.>

## Inputs / upstream state
<Only design-relevant prerequisites.>

## Accepted design
<Current objects/states/relationships/semantics.>

## Invariants / trust boundaries
<Only when material.>

## Lifecycle / transitions
<Only when applicable.>

## Ownership and interfaces
<Adjacent owners and handoff semantics.>

## Design acceptance
<Conditions showing this concern is specified enough to project/implement.>
```

Headings are optional. Remove empty sections rather than filling `N/A`.

## Dynamic restructuring checklist

Before creating a new topic, ask:

```text
Does it have an independent responsibility?
Can its semantics be owned without another file redefining them?
Does it have a distinct interface/state/trust/consumer/change lifecycle?
Will splitting reduce unrelated context for normal readers?
```

Before splitting:

```text
Are there multiple independent concerns currently forced into one owner?
Would each resulting file have a stable semantic owner?
Can ordinary tasks read one without mandatory chains through the others?
```

Before merging:

```text
Do the files always need to be read/changed together?
Do they duplicate semantics or repeatedly cross-reference each other?
Would one coherent owner be clearer and cheaper to load?
```

After any accepted restructuring:

```text
update README.md
→ keep only current topic files
→ remove superseded design files from design/
→ renumber for clean current reading order when useful
→ preserve semantic identity through design_id
→ project the accepted change into SKILL/references before implementation
```

## Current-state-only check

Reject a living-design file if it contains material whose primary purpose is historical reconstruction, including:

```text
old design copies
rejected alternatives
chronological decision narrative
"previous version" sections
implementation progress logs
test result history
Codex execution detail
```

Those belong in `reports/concept/`, Git history, tasks, reports, or another proper owner.
