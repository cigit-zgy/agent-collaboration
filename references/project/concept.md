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

When a project declares `reports/concept/` as design authority, each concept topic is the canonical design for one bounded concern after User + ChatGPT design/adjudication and User acceptance.

The authority chain is:

```text
reports/concept/
→ SKILL.md + references/
→ scripts/code/schemas
→ tests/
→ runtime artifacts
```

Downstream artifacts conform to the governing concept. A mismatch is projection or implementation drift unless a design change is reviewed/adjudicated by User + ChatGPT and accepted by the User first.

Scientific fact authority remains separate:

```text
project design truth   = reports/concept/
model scientific facts = registered source + evidence/provenance
```

A concept defines how the project represents, validates, or operates on scientific information. Model-specific values, equations, symbols, and claims remain grounded in the registered source/evidence chain.

## Concept writing standard

### Core objective

A concept topic should let an unfamiliar reader recover the accepted design without reconstructing prior discussion or reading current implementation.

The following information should be recoverable when applicable:

1. why the design object, stage, or concern exists;
2. its responsibility and boundary;
3. its required inputs or upstream state;
4. the state, object, interface, or architecture it establishes;
5. its lifecycle or state transitions when these are part of the design;
6. ownership and downstream consumers;
7. the condition under which the designed stage/object is considered valid or complete;
8. the interface or handoff to adjacent stages or concerns.

These are information requirements, not mandatory Markdown headings.

### Declarative design, not an execution manual

Write the accepted system state and semantics declaratively.

Preferred:

```text
A registered artifact has one canonical identity within its owning scope.
A preserved source artifact remains byte-identical across downstream read-only use.
```

Use procedural wording only when ordering, interaction, or transition is itself part of the accepted design.

Detailed Agent instructions belong to `SKILL.md`; detailed bounded operational contracts belong to `references/`; implementation mechanics belong to code/schema.

### One topic, one design owner

Each concept topic owns one coherent design concern. Cross-topic relationships may be stated at interfaces, but the same design rule should not be independently redefined in several concept files.

`reports/concept/README.md` maps the design topics and their operational projections.

### Current solution only

A canonical concept contains the current accepted solution. It does not serve as:

- chat or decision chronology;
- implementation journal;
- Codex task/report;
- test-result store;
- transient filesystem/worktree state;
- backlog of unaccepted alternatives;
- container for model-specific scientific facts copied from sources.

Historical evolution is preserved by Git history and formal collaboration reports.

### Design-level specificity

Include enough detail to constrain downstream projections and make conformance auditable. Avoid implementation detail that has no design consequence.

A useful distinction is:

```text
Design consequence     → concept
Agent execution detail → SKILL/reference
Code mechanism         → implementation
Observed evidence      → test/report/runtime artifact
```

### Recommended shape

Use the smallest structure that communicates the accepted design. A common stage-oriented shape is:

```markdown
# <Design topic>

## Purpose

<Why this concern exists and the stable outcome it establishes.>

## Boundary

<What this topic owns and where adjacent ownership begins.>

## Inputs / upstream state

<Only design-relevant prerequisites.>

## Accepted design

<Objects, states, relationships, semantics, and invariants.>

## Lifecycle / transitions

<Only when lifecycle is part of the design.>

## Ownership and interfaces

<Producer/owner/consumer and adjacent-stage handoff.>

## Design acceptance

<Directly assessable conditions showing the design is internally complete enough to project.>
```

The headings are optional. Structure follows the design concern rather than a fixed template.

## Concept index

`reports/concept/README.md` is the design map. It identifies active design topics and the downstream operational files that project each topic. It is not an implementation-status board.

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

Metadata should remain minimal and should not duplicate body semantics.

## Review, adjudication, freeze, and projection

External review is evidence, not design authority.

The normal design lifecycle is:

```text
current canonical concept
→ adversarial / expert / implementation review
→ findings
→ User + ChatGPT adjudication
→ User decision
   ├── reject change → concept unchanged
   └── accept change → concept updated
→ design freeze for the current concern
→ SKILL/reference projection
→ implementation
→ conformance verification
```

Reviewers, Codex, tests, and existing implementation may expose defects, contradictions, or missing requirements. They do not directly redefine the canonical design.

### Adjudication

User + ChatGPT review and adjudicate whether a finding should change the accepted solution. The User retains final acceptance/override authority. A proposed change becomes design only after the User accepts it and the governing concept is updated.

An implementation mismatch is therefore handled as:

```text
concept = A
projection/code = B

→ inspect whether B is drift or whether A should change
→ User + ChatGPT adjudicate
→ User decides whether the accepted design changes
→ if A remains accepted, repair B
→ if design changes, update A first and then propagate downstream
```

### Freeze

A design concern is frozen when:

```text
its responsibility and boundary are clear
AND the current solution has been reviewed/adjudicated by User + ChatGPT
AND the current solution is accepted by the User
AND blocking design ambiguities for the intended scope are resolved
AND downstream projection can be written without inventing new design semantics
```

Freeze means the current design is stable enough to project and implement. It does not mean the design can never change, that implementation is complete, or that scientific validation has already succeeded.

`freeze` is a collaboration lifecycle condition, not a required metadata enum or additional state file.

### Reopening a frozen design

A frozen concept is reopened only when new evidence or a new User requirement materially changes the accepted design. User + ChatGPT adjudicate the change; the User decides whether to accept it. The concept is updated first, then re-frozen for the revised scope, and only then are Skills/references/code/tests updated.

Routine implementation discoveries that do not change design remain downstream implementation work.

## Reading paths

Routine execution may use the already-derived operational projection:

```text
AGENTS.md
→ workflow SKILL.md
→ owning sub-Skill
→ required reference/script
```

Design, redesign, adversarial design review, stage reconstruction, or conformance audit begins from the governing concept:

```text
AGENTS.md
→ reports/concept/README.md
→ relevant concept topic(s)
→ affected SKILL/reference projection
→ implementation/tests as needed
```

## Collaboration-repository exception

`agent-collaboration` itself is a protocol/Skill repository. Its active policy lives in `references/`; its existing `reports/concept/` files are decision history/rationale rather than canonical project design.

Task/report metadata formats live in `../collaboration/templates/chatgpt-task.md` and `../collaboration/templates/codex-report.md`.
