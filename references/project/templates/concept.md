# Project concept authoring template

Cold path: load this file only when creating or materially rewriting a project's canonical concept topic.

Concept authority/freeze/reopen/adjudication semantics are owned by `../concept.md`.

## Writing objective

A concept topic should let an unfamiliar reader recover the accepted design without reconstructing prior discussion or reading current implementation.

Make these recoverable when applicable:

1. why the design object/stage/concern exists;
2. responsibility and boundary;
3. required inputs/upstream state;
4. state/object/interface/architecture established;
5. lifecycle/state transitions when design-relevant;
6. ownership and downstream consumers;
7. validity/completion condition;
8. interface/handoff to adjacent concerns;
9. for prior-art-gated design, external precedent and reuse/custom-gap decision.

These are information requirements, not mandatory headings.

## Declarative design

Write accepted system state and semantics declaratively.

Preferred:

```text
A registered artifact has one canonical identity within its owning scope.
A preserved source artifact remains byte-identical across downstream read-only use.
```

Use procedural wording only when ordering, interaction, or transition is itself part of accepted design.

Detailed Agent instructions belong to `SKILL.md`; operational contracts belong to references; implementation mechanics belong to code/schema; observed evidence belongs to tests/reports/runtime artifacts.

## One topic, one design owner

Each concept topic owns one coherent design concern. Cross-topic relationships may be stated at interfaces, but the same design rule should not be independently redefined in several concept files.

`reports/concept/README.md` maps active design topics and downstream projections. It is a design map, not an implementation-status board.

## Current solution only

A canonical concept contains the current accepted solution. It is not:

```text
chat/decision chronology
implementation journal
Codex task/report
test-result store
transient filesystem/worktree state
backlog of unaccepted alternatives
container for model-specific scientific facts copied from sources
```

Historical evolution is preserved by Git history and formal collaboration reports.

## Design-level specificity

Include enough detail to constrain downstream projections and make conformance auditable. Avoid implementation detail without design consequence.

```text
Design consequence     → concept
Agent execution detail → SKILL/reference
Code mechanism         → implementation
Observed evidence      → test/report/runtime artifact
```

## Prior-art basis

For gate-triggered design, include a compact basis containing:

```text
search scope
strongest materially relevant precedents
source/repository coordinates
REUSE | ADAPT | REFERENCE_ONLY | REJECT disposition
design consequence
remaining project-specific gap
```

Do not turn the concept into a literature review. Detailed search policy is owned by `../prior-art.md`.

## Recommended shape

Use the smallest structure that communicates the accepted design. A common stage-oriented shape is:

```markdown
# <Design topic>

## Purpose
<Why this concern exists and the stable outcome it establishes.>

## Boundary
<What this topic owns and where adjacent ownership begins.>

## Inputs / upstream state
<Only design-relevant prerequisites.>

## Prior-art basis
<Only for gate-triggered design.>

## Accepted design
<Objects, states, relationships, semantics, invariants.>

## Lifecycle / transitions
<Only when lifecycle is part of the design.>

## Ownership and interfaces
<Producer/owner/consumer and adjacent-stage handoff.>

## Design acceptance
<Directly assessable conditions showing internal completeness for projection.>
```

Headings are optional; structure follows the concern.

## Minimal metadata

A topic may use:

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

Metadata stays minimal and does not duplicate body semantics.

## Authoring quality check

A concept is well written when:

```text
accepted design is recoverable without chat reconstruction
one topic has one owner
current solution is separated from history/backlog
prior-art basis is compact but recoverable when required
scientific facts remain source-grounded
projection can be written without inventing missing semantics
```
