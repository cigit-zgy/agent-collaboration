# Project living-design contract

Load this reference for the canonical current project design under `design/`: dynamic topic decomposition, ownership, file naming, current-state-only semantics, and projection into Skills/code/tests.

`reports/concept/` is the chronological design journal and is owned by `concept.md`. It records how the design was explored. `design/` records only the current accepted result.

## Core distinction — hard boundary

```text
reports/concept/
= what we considered, questioned, compared, rejected, or gradually clarified
= chronological design journal
= may be incomplete, exploratory, contradictory, or later superseded
= never current design authority

design/
= what the project currently accepts
= canonical living design authority
= structured by current responsibilities, not chronology
= exactly one current design set
= no historical versions inside the directory
```

Git history and `reports/concept/` preserve historical evolution. `design/` MUST NOT keep copies such as `old`, `backup`, `v2`, dated snapshots, superseded files, or parallel alternative designs.

## Stable top-level shape

A maintained project that uses explicit design authority uses:

```text
design/
├── README.md
├── 00_overview.md          # required when the design has multiple concerns or system-level topology matters
├── 01_<semantic-topic>.md
├── 02_<semantic-topic>.md
└── ...                     # count is dynamic
```

`README.md` is a navigation map only. It identifies the current design files, their `design_id`, one-line responsibility, and direct reading route. It MUST NOT restate design semantics or become a second authority.

`00_overview.md` owns only whole-system scope, major components/stages, top-level relationships, and the design map needed to understand how topic files fit together. Detailed semantics stay in the owning topic file.

For a very small project with one coherent design concern, `README.md` plus one topic file may be sufficient; do not create `00_overview.md` merely for symmetry.

## Dynamic topic decomposition

The number and names of topic files are project-specific and may change as the design matures.

Create a new topic file only when the candidate concern has a real independent design responsibility. Strong signals are:

```text
it has a distinct purpose/boundary
AND it owns semantics that can be stated without another file redefining them
AND it has a distinct interface, state, trust boundary, consumer, or change lifecycle
AND separating it lets a reader load less unrelated design context
```

Do NOT split merely because a file is long. Keep one coherent concern together when splitting would create mandatory multi-file reading for ordinary understanding.

### Update an existing topic

A new concept normally updates an existing design topic when it refines or changes semantics already owned by that topic without creating a new independent responsibility.

### Split

Split one topic into several when it has accumulated independent responsibilities with different boundaries, consumers, interfaces, or change lifecycles.

After splitting:

```text
one former owner
→ several non-overlapping current owners
→ README.md updated
→ old combined file removed from design/
```

History remains in Git and the concept journal; do not retain the old combined file in `design/`.

### Merge

Merge topics when they cannot be understood or changed independently and their separation creates duplicate semantics or mandatory cross-reading.

After merging, remove the superseded topic files from `design/`. Do not leave redirects/stubs unless a real external consumer requires one and the project explicitly accepts that compatibility contract.

### Add / remove / reorder

A topic may be added, removed, or reordered whenever the accepted current architecture changes.

Number prefixes represent current reading order only. They are not semantic identity. When the current design map changes materially, renumber files into a clean contiguous order when that improves navigation.

Stable semantic identity lives in `design_id`, not in `01_`, `02_`, etc.

## Concept → design reduction

Every material concept journal entry is treated as design input, not as a new design version.

After User + ChatGPT adjudication, classify its effect on the current design:

```text
NO_CHANGE
= useful historical reasoning, but accepted design remains unchanged

UPDATE
= revise one or more existing topic files

NEW_TOPIC
= introduce a genuinely independent design concern

SPLIT
= decompose an overloaded current owner

MERGE
= combine owners whose separation is no longer meaningful

REMOVE
= current design no longer contains a concern

REORDER
= current reading/topology order changes without semantic duplication
```

Then rewrite `design/` into the new current normal form.

There is no one-to-one correspondence between concept files and design files:

```text
many concept notes may reduce into one design update
one concept note may update several design topics
some concept notes may produce no design change
one accepted concept may cause a topic split/merge/reorder
```

## Single-current-set invariant — hard requirement

At every accepted repository state:

```text
one design concern
→ exactly one current owner in design/

one current project design
→ exactly one design/ tree
```

The following are non-conforming:

```text
design_v2/
design_old/
design/draft/
design/archive/
design/01_xxx_old.md
design/01_xxx_20260907.md
parallel A/B design files representing competing current schemes
same semantic rule independently defined in multiple topic files
```

Unaccepted alternatives stay in `reports/concept/`; superseded accepted designs remain recoverable through Git history.

## Topic filename and identity

Current topic files use:

```text
NN_<semantic-topic>.md
```

with two-digit `NN`. Prefer lowercase snake_case or the repository's established semantic naming convention consistently.

Each topic begins with compact metadata:

```yaml
---
design_id: <stable-semantic-id>
title: <human-readable title>
status: active
role: design_authority
summary: >
  <one compact statement of the concern owned by this file>
operational_projection:
  - <path>   # optional; include only real downstream projections
---
```

Do not add dates, version numbers, `previous_version`, supersession chains, decision chronology, or implementation status to living-design metadata. Those are historical/execution concerns.

## Topic content architecture

A topic file should make the following recoverable when applicable:

1. **Purpose** — why this current responsibility exists;
2. **Boundary** — what it owns and explicitly does not own where ambiguity is plausible;
3. **Inputs / upstream state** — only design-relevant prerequisites;
4. **Accepted design** — current objects, states, semantics, relationships, algorithms, or policies;
5. **Invariants / trust boundaries** — only when they materially constrain the design;
6. **Lifecycle / transitions** — only when state evolution is part of the concern;
7. **Ownership and interfaces** — adjacent owners and handoff semantics;
8. **Design acceptance** — directly assessable conditions showing this concern is sufficiently specified for projection.

These are information requirements, not mandatory headings. Use the smallest structure that makes the current design unambiguous.

A living-design file MUST NOT become:

```text
a discussion diary
a list of rejected alternatives
a dated decision log
a Codex task/report
a test-result store
an implementation-status board
a backlog
an archive
```

Current rationale that is necessary to interpret semantics may be stated briefly. Historical argumentation belongs in `reports/concept/`.

## Overview architecture

When present, `00_overview.md` should stay compact and own only cross-cutting system structure:

```text
project/system purpose
whole-system architecture or stage graph
major stable objects/domains
cross-topic trust or authority boundaries that are genuinely global
current topic map and relationships
whole-design acceptance/completion condition when one exists
```

It MUST NOT duplicate the detailed contract of each numbered topic file.

## Atomic current-design update

When one accepted concept affects several design files, update the affected design topics and `README.md` as one coherent design change before downstream projection.

Do not intentionally leave a mixed state where some files express the new design and others still express the superseded design.

## Projection order

Accepted design flows downward:

```text
reports/concept/ input/evidence/history
→ User + ChatGPT adjudication
→ design/ current canonical state
→ SKILL.md + references
→ scripts/code/schema/config
→ tests/evaluation
→ runtime artifacts
```

Codex implements the committed current design/Skill projection. Tests may expose a `DESIGN_GAP`, but they do not silently redefine `design/`.

## Reading discipline

For design work, start at:

```text
design/README.md
→ 00_overview.md only when whole-system context is needed
→ one or more directly relevant topic files
```

Do not preload all design topics for a bounded concern. Do not read `reports/concept/` unless reconstructing rationale/history, adjudicating a new idea, or resolving an explicit design question.

## Completion

The living design is well formed when:

```text
README.md maps every current topic once
AND every current concern has exactly one owner
AND file count reflects real responsibilities rather than a fixed template
AND no historical/alternative design copy remains under design/
AND topic files express only current accepted semantics
AND downstream Skill/reference projection can proceed without inventing missing design choices
```
