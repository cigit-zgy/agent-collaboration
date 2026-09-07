# Project concept authoring template

Cold path: load this file only when creating or materially rewriting a project's canonical concept topic.

Concept authority/freeze/reopen/adjudication semantics are owned by `../concept.md`; report filenames and common metadata by `../reports.md`.

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

Write accepted system state and semantics declaratively. Detailed Agent instructions belong to `SKILL.md`; operational contracts belong to references; implementation mechanics belong to code/schema; observed evidence belongs to tests/reports/runtime artifacts.

## One topic, one design owner

Each concept topic owns one coherent design concern. Cross-topic relationships may be stated at interfaces, but the same design rule should not be independently redefined in several concept files.

Concept discovery uses canonical filename chronology plus YAML `concept_id`, title, status and summary. Do not create `README.md` or semantic-filename exceptions under `reports/concept/`.

## Current solution only

A canonical concept contains the current accepted solution. It is not a chat chronology, implementation journal, Codex task/report, test-result store, transient filesystem state, backlog of unaccepted alternatives, or a container for model-specific scientific facts copied from sources.

Historical evolution is preserved by Git history and formal collaboration artifacts; displaced legacy files follow the root `00_archive/` policy in `../reports.md`.

## Design-level specificity

Include enough detail to constrain downstream projections and make conformance auditable. Avoid implementation detail without design consequence.

```text
Design consequence     → concept
Agent execution detail → SKILL/reference
Code mechanism         → implementation
Observed evidence      → test/report/runtime artifact
```

## Prior-art basis

For gate-triggered design, include a compact basis containing search scope, strongest relevant precedents, source/repository coordinates, `REUSE | ADAPT | REFERENCE_ONLY | REJECT` disposition, design consequence, and remaining project-specific gap. Do not turn the concept into a literature review.

## Recommended shape

Use the smallest structure that communicates the accepted design. A common stage-oriented shape is:

```markdown
# <Design topic>

## Purpose
## Boundary
## Inputs / upstream state
## Prior-art basis
## Accepted design
## Lifecycle / transitions
## Ownership and interfaces
## Design acceptance
```

Headings are optional; structure follows the concern.

## Required metadata

Every concept file begins with:

```yaml
---
artifact_type: project_concept
artifact_id: <YYMMDD_concept_NN>
title: <TITLE>
date: <YYYY-MM-DD>
project: <PROJECT_NAME>
repository: <OWNER/REPOSITORY>
status: <active | frozen | designing | superseded>
summary: >
  <compact searchable summary>
concept_id: <STABLE_SEMANTIC_CONCERN_ID>
role: design_authority
operational_projection:
  - <path>
---
```

`artifact_id` equals the filename stem. `concept_id` is the stable semantic identity and may remain unchanged across later revisions. Additional topic-specific metadata is allowed when it carries real navigation/authority value, but metadata must not duplicate the body.

## Authoring quality check

A concept is well written when accepted design is recoverable without chat reconstruction, one topic has one owner, current solution is separated from history/backlog, scientific facts remain source-grounded, and projection can be written without inventing missing semantics.
