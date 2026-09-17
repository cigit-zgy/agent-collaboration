# Project living-design contract

Load this reference for the canonical current project Design under `reports/design/`: ownership, topic decomposition, naming, current-state semantics, and projection into Skills/code/tests.

Historical work lives in Reports. Current accepted semantics live here. Opportunistic project-entry synchronization is owned by `reconciliation.md`.

## Core boundary

```text
reports/design/
= what the project currently accepts
= one mutable current normal form
= current authority

reports/chatgpt/ + reports/codex/ + reports/concept/
= append-only historical work/evidence
= never current Design authority
```

Do not keep parallel root `design/`, dated Design snapshots, drafts, backups, old versions, or superseded current owners.

## One concern, one owner

Every active Design concern has exactly one current owner.

A topic is non-conforming when it mainly exists to supersede, refine, override, or preserve another current topic for the same semantic responsibility. Merge accepted semantics into the real owner and remove the duplicate current file.

A bounded concern normally reads:

```text
one primary Design owner
+ at most one genuinely necessary secondary owner
```

Persistent three-plus-owner reading chains are Design architecture drift.

## Default normal form

A mature project normally needs roughly 5–8 topics. Use semantic responsibilities rather than chronology.

A useful default decomposition is:

```text
reports/design/
├── README.md
├── 00_overview.md
├── 01_domain_and_objects.md
├── 02_workflow_and_state.md
├── 03_artifacts_and_ownership.md
├── 04_interfaces.md
├── 05_trust_and_validation.md
└── 06_runtime_and_skills.md
```

These names are defaults, not mandatory filenames. Merge, rename, or omit topics when the project has fewer real responsibilities.

Topic-count guard:

```text
5–8 current topics      healthy default
adding topic 9+         inspect for consolidation first
> 12 current topics     no additional topic by default; consolidate first
```

Exceeding 12 requires explicit User approval or a clearly independent responsibility that cannot be merged without harming ownership clarity.

## README.md

`reports/design/README.md` is navigation plus compact Design-maintenance metadata only.

It may contain:

```text
design_id
file
one-line responsibility
short reading hint
Design reconciliation cursor from reconciliation.md
```

The project root `AGENTS.md` owns the trigger hook. README stores only the cursor/state needed to make the project-entry check cheap.

It must not restate detailed Design semantics or become a progress log.

## Topic identity

Current topic files use `NN_<semantic-topic>.md`; the numeric prefix is reading order only. Stable identity lives in `design_id`.

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

Do not encode dates, version chains, implementation status, task state, or test history in topic metadata.

## Topic creation gate

Create a new topic only when it has an independent responsibility with a distinct boundary and stable consumer/interface/state/trust/change lifecycle.

Do not create a topic merely because a file is long, a task produced a result, one model needs a correction, a new conversation started, or a more specific filename seems convenient.

## Mutable current-state rule

When accepted Design changes:

```text
update the owning topic(s) in the same work unit
→ merge/split/remove/reorder only when responsibility changes
→ update README routing when needed
→ remove superseded current semantics
```

Do not wait for a later reconciliation when the accepted consequence is already known.

History stays in Git and append-only Reports. Design never becomes a discussion diary, task report, test store, backlog, progress board, or archive.

## Runtime and Skill profile

For projects with multiple reusable Skills, current Skill selection belongs to one Design owner, normally `runtime_and_skills` or an equivalent concern.

Record only what future Agents need to choose correctly:

```text
Skill / tool
immutable authority or source when applicable
activation condition
required | conditional
purpose
```

Do not copy the Skill manuals into Design. `AGENTS.md` should route to this owner rather than maintain a second Skill-profile truth.

## Reports and historical rationale

A current topic may cite exact ChatGPT/Codex/Concept report paths when historical provenance is useful, but current semantics must remain understandable from Design without reconstructing history.

Concept creation remains subject to the explicit User gate in `concept.md`.

## Projection

```text
reports/design/
→ SKILL.md + references
→ scripts/code/schema/config
→ tests/evaluation
→ runtime artifacts
```

Tests and reports may expose a Design gap; they do not silently redefine Design.

## Self-hosting Skill-repository exception

When a repository's maintained product is itself an operational Skill/policy and `SKILL.md + references/` are intentionally the canonical current operational contract, do not duplicate the same current semantics into `reports/design/` merely for symmetry.

For such a self-hosting repository, including `agent-collaboration` itself:

```text
SKILL.md + references/ = current operational authority
reports/chatgpt/ + reports/codex/ + reports/concept/ = historical work/evidence
```

Use `reports/design/` only if the repository has a genuinely separate project Design responsibility.

## Completion

Living Design conforms when there is one current normal form, every concern has one owner, topic count remains justified, current Skill/runtime selection has one owner when needed, accepted changes are synchronized promptly, and downstream work can proceed without reconstructing report history.
