# Project living-design contract

Load this reference for the canonical current project design under `reports/design/`: dynamic topic decomposition, ownership, naming, current-state-only semantics, and projection into Skills/code/tests.

`reports/concept/` records how the design was explored. `reports/design/` records only the current accepted result.

## Core distinction — hard boundary

```text
reports/concept/
= what we considered, questioned, compared, rejected, or clarified
= chronological design history/input
= never current design authority

reports/design/
= what the project currently accepts
= canonical living design authority
= structured by current responsibilities, not chronology
= exactly one current design set
= no historical versions inside
```

Git history plus `reports/concept/` preserve evolution. Do not keep `old`, `backup`, `v2`, dated snapshots, drafts, or parallel alternatives inside `reports/design/`.

## Reports/design is not a report family

`reports/design/` is co-located under `reports/` for repository compactness, but it is not governed by chronological report-family filename/metadata rules.

The `YYMMDD_<family>_NN.md`, flat-family, and report metadata rules apply only to:

```text
reports/chatgpt/
reports/codex/
reports/concept/
reports/handoff/
```

They do not apply to `reports/design/`.

## Stable shape

```text
reports/design/
├── README.md
├── 00_overview.md          # only when whole-system context is needed
├── 01_<semantic-topic>.md
├── 02_<semantic-topic>.md
└── ...                     # dynamic count
```

`README.md` is navigation only: current design files, `design_id`, one-line responsibility, and direct reading route. It must not restate topic semantics.

`00_overview.md` owns only whole-system scope/topology and cross-topic relationships. Detailed semantics stay in topic owners.

## Dynamic decomposition

Create a new topic only when it has a real independent responsibility: distinct purpose/boundary, independently owned semantics, a distinct interface/state/trust/consumer/change lifecycle, and a split that reduces unrelated context.

Do not split merely because a file is long.

Accepted concept effects are:

```text
NO_CHANGE
UPDATE
NEW_TOPIC
SPLIT
MERGE
REMOVE
REORDER
```

Many concept notes may reduce into one design update; one concept note may update several topics.

After split/merge/remove/reorder, rewrite `reports/design/` into one clean current state and update `README.md`. Remove superseded current-design files; history remains in Git/concept notes.

## Single-current-set invariant

```text
one design concern
→ exactly one current owner in reports/design/

one current project design
→ exactly one reports/design/ tree
```

Non-conforming examples:

```text
reports/design_v2/
reports/design_old/
reports/design/draft/
reports/design/archive/
reports/design/01_xxx_old.md
reports/design/01_xxx_20260907.md
parallel A/B current designs
same semantic rule defined independently in multiple topic files
```

## Topic identity

Current topic files use:

```text
NN_<semantic-topic>.md
```

with two-digit `NN`. Numeric prefixes are reading order only; stable identity lives in `design_id`.

Each topic begins with compact metadata:

```yaml
---
design_id: <stable-semantic-id>
title: <human-readable title>
status: active
role: design_authority
summary: >
  <one compact statement of the concern>
operational_projection:
  - <real downstream path when useful>
---
```

Do not put dates/version chains/implementation status in living-design metadata.

## Topic content

When applicable, make these recoverable:

```text
purpose
boundary
inputs / upstream state
accepted design
invariants / trust boundaries
lifecycle / transitions
ownership and interfaces
design acceptance
```

Use the smallest structure that makes current semantics unambiguous.

A design file must not become a discussion diary, rejected-alternative list, test store, task/report, backlog, progress board, or archive.

## Atomic update and projection

When one accepted concept affects several topics, update all affected `reports/design/` files plus `README.md` coherently before downstream projection.

Accepted design flows:

```text
reports/concept/ input/history
→ User + ChatGPT adjudication
→ reports/design/ current authority
→ SKILL.md + references
→ scripts/code/schema/config
→ tests/evaluation
→ runtime artifacts
```

Tests may expose `DESIGN_GAP`; they do not silently redefine design.

## Reading discipline

```text
reports/design/README.md
→ 00_overview.md only when whole-system context is needed
→ directly relevant topic file(s)
```

Do not preload all topics. Read `reports/concept/` only for rationale/history or an explicit design question.

## Completion

The living design is healthy when `README.md` maps every current topic once, every concern has one owner, no historical/alternative copy remains under `reports/design/`, and downstream projection can proceed without inventing missing design choices.
