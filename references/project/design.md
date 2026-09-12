# Project living-design contract

Load this reference for the canonical current project design under `reports/design/`: ownership, current-state semantics, topic decomposition, naming, and projection into Skills/code/tests.

`reports/concept/` is explicit User-requested historical reasoning only. Project-wide admission/drift checks are owned by `governance.md`.

## Core boundary

```text
reports/design/
= what the project currently accepts
= exactly one current design set
= mutable current state

reports/concept/
= dated historical reasoning
= append-only when explicitly requested by the User
= never current authority
```

## Single current set

Use exactly one:

```text
reports/design/
```

Do not keep parallel root `design/`, `design_v2/`, dated design trees, drafts, backups, or archived current-design copies.

## One concern, one owner

Every active design concern has exactly one current owner.

A current topic is non-conforming when it mainly exists to supersede, refine, override, or preserve a previous current topic for the same semantic responsibility. Merge the accepted semantics into the real owner and remove the superseded current file.

Cross-topic interfaces are allowed. Duplicate ownership is not.

For bounded work, the normal current-design read set is one primary owner plus at most one genuinely necessary secondary owner. If one rule routinely requires three or more current design topics to establish its meaning, treat that as `DESIGN_ARCHITECTURE_DRIFT` under `governance.md` and consolidate ownership before adding more topics.

## Shape

```text
reports/design/
├── README.md
├── 00_overview.md          # only when whole-system topology is genuinely needed
├── 01_<semantic-topic>.md
├── 02_<semantic-topic>.md
└── ...
```

`README.md` is navigation only: `design_id`, file, one-line responsibility, and short reading hints. It does not restate detailed design semantics.

`00_overview.md` owns only cross-topic system scope/topology. Do not use it as a second copy of detailed topic rules.

## Topic creation gate

Create a new topic only when it has an independent responsibility with a distinct purpose/boundary and a stable consumer/interface/state/trust/change lifecycle. Splitting must reduce unrelated context.

Do not create a topic merely because:

```text
a model or dataset needs one correction
a task produced a result
a current file is long
a new conversation started
a current topic can be described more specifically in another file
```

Model-specific scientific facts normally belong to source/model/golden authority, not project living design.

## Mutable current-state rule

Design is current-only and replace-in-place.

When accepted design changes:

```text
update/overwrite the owning current topic(s)
→ merge/split/remove/reorder when responsibility changes
→ update README.md
→ remove superseded current design files
```

History is preserved by Git and, only when explicitly requested by the User, new dated Concept artifacts. Do not preserve old Design beside the replacement.

## Explicit Concept coupling

When the User explicitly asks to persist a decision in Concept, `concept.md` requires a new dated Concept file and a same-work-unit update to current Design. Concept is append-only; Design is mutable current state.

## Topic identity

Current topic files use:

```text
NN_<semantic-topic>.md
```

with two-digit reading-order prefixes. Stable identity lives in `design_id`, not the number.

Each topic begins with compact metadata:

```yaml
---
design_id: <stable-semantic-id>
title: <human-readable title>
status: active
role: design_authority
summary: >
  <one compact statement of the owned concern>
operational_projection:
  - <real downstream path when useful>
---
```

Do not encode dates, version chains, supersession history, implementation status, task status, or test history in living-design metadata.

## Content boundary

A topic may own purpose, boundary, accepted semantics, interfaces, invariants, lifecycle, and design acceptance when relevant.

It must not become a discussion diary, scientific qualification report, model-specific fact store, task/report, test store, backlog, progress board, or archive.

## Projection

Accepted current Design flows downward:

```text
reports/design/
→ SKILL.md + references
→ scripts/code/schema/config
→ tests/evaluation
→ runtime artifacts
```

Tests may expose a `DESIGN_GAP`; they do not redefine current Design silently.

## Reading discipline

```text
reports/design/README.md
→ one primary current topic
→ at most one necessary secondary current topic
```

Read Concept history only for an explicit historical-rationale need. Do not preload all Design topics or all Concepts.

## Completion

Living Design conforms when there is one `reports/design/` tree, every current concern has one owner, no superseded/parallel owner remains, bounded concerns do not require multi-owner reading chains, and downstream projection can proceed without inventing missing semantics.
