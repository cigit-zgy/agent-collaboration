# Project concept and report policy

This contract governs formal collaboration reports and `reports/concept/` for maintained scientific/research projects.

## Stable report layout

```text
reports/
├── concept/   current accepted project design
├── chatgpt/   committed local-execution specifications
├── codex/     execution and verification evidence
└── handoff/   conversation continuity/context recovery; not design/task authority
```

Formal task/report paths remain stable after issue. Conversation handoff artifact/index semantics are owned by `handoff.md`.

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

Conversation handoffs may summarize the design and project state for migration, but they are reconstruction context only. A handoff never becomes a substitute for the governing concept, task, or scientific source/evidence.

## External prior-art gate — hard requirement

Before freezing a concept for a new maintained project, new core subsystem, major algorithm/modeling method, major architecture redesign, important trust/provenance mechanism, or substantial framework/tool choice, User + ChatGPT MUST complete the external prior-art gate in `prior-art.md`.

The gate requires both:

```text
authoritative literature → linked/open implementation
AND
GitHub/source implementation → scientific/institutional provenance
```

The concept MUST record a compact prior-art basis: the search scope, strongest materially relevant candidates, their provenance/source coordinates, `REUSE | ADAPT | REFERENCE_ONLY | REJECT` disposition, and the remaining project-specific gap that justifies custom design.

External prior art is evidence, not project authority. User + ChatGPT decide what to adopt; the accepted concept remains the project design authority.

If the gate applies but the prior-art basis is not recoverable, the concept is not ready to freeze and substantial custom implementation must not begin merely because an internal solution can be imagined quickly.

Routine bug fixes, small bounded refactors, and implementation under an unchanged accepted design do not repeat the full gate.

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
8. the interface or handoff to adjacent stages or concerns;
9. for gate-triggered design, the external prior-art basis and reuse/custom-gap decision.

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
- conversation-migration/context summary;
- implementation journal;
- Codex task/report;
- test-result store;
- transient filesystem/worktree state;
- backlog of unaccepted alternatives;
- container for model-specific scientific facts copied from sources.

Historical evolution is preserved by Git history and formal collaboration reports. Conversation continuity belongs in `reports/handoff/` under `handoff.md`.

### Design-level specificity

Include enough detail to constrain downstream projections and make conformance auditable. Avoid implementation detail that has no design consequence.

A useful distinction is:

```text
Design consequence       → concept
Conversation continuity  → handoff
Agent execution detail   → SKILL/reference
Code mechanism           → implementation
Observed evidence        → test/report/runtime artifact
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

## Prior-art basis

<For gate-triggered design: strongest relevant external precedents, dispositions, and design consequence.>

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

`reports/concept/README.md` is the design map. It identifies active design topics and the downstream operational files that project each topic. It is not an implementation-status board or conversation-handoff index.

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

External review and prior art are evidence, not design authority.

For a gate-triggered concern, the normal design lifecycle is:

```text
problem / design concern
→ prior-art.md search + candidate inspection
→ reuse/adapt/reference/reject dispositions
→ current canonical concept
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

For routine redesign where the prior-art gate is not triggered, the lifecycle may begin at the current canonical concept.

Reviewers, prior-art sources, Codex, tests, existing implementation, and conversation handoffs may expose defects, contradictions, missing requirements, proven patterns, or historical rationale. They do not directly redefine the canonical design.

### Adjudication

User + ChatGPT review and adjudicate whether a finding or external precedent should change the accepted solution. The User retains final acceptance/override authority. A proposed change becomes design only after the User accepts it and the governing concept is updated.

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
AND any applicable prior-art gate is complete and recorded
AND the current solution has been reviewed/adjudicated by User + ChatGPT
AND the current solution is accepted by the User
AND blocking design ambiguities for the intended scope are resolved
AND downstream projection can be written without inventing new design semantics
```

Freeze means the current design is stable enough to project and implement. It does not mean the design can never change, that implementation is complete, or that scientific validation has already succeeded.

`freeze` is a collaboration lifecycle condition, not a required metadata enum or additional state file.

### Reopening a frozen design

A frozen concept is reopened only when new evidence or a new User requirement materially changes the accepted design. When the reopening introduces a new major design concern or substantially changes method/tool choice, repeat the relevant prior-art gate. User + ChatGPT adjudicate the change; the User decides whether to accept it. The concept is updated first, then re-frozen for the revised scope, and only then are Skills/references/code/tests updated.

Routine implementation discoveries that do not change design remain downstream implementation work.

## Reading paths

Routine execution may use the already-derived operational projection:

```text
AGENTS.md
→ workflow SKILL.md
→ owning sub-Skill
→ required reference/script
```

Context recovery after conversation migration uses the navigation owner in `handoff.md`:

```text
AGENTS.md
→ reports/handoff/README.md
→ current handoff only
→ current project/collaboration authority
→ then the relevant routine/design route
```

New project design or gate-triggered redesign begins with:

```text
AGENTS.md
→ reports/concept/README.md
→ references/project/prior-art.md
→ external evidence + strongest implementation precedents
→ relevant concept topic(s)
→ affected SKILL/reference projection
→ implementation/tests as needed
```

Design/redesign/adversarial review that does not trigger a new prior-art search may begin from the governing concept directly.

## Collaboration-repository exception

`agent-collaboration` itself is a protocol/Skill repository. Its active policy lives in `references/`; its existing `reports/concept/` files are decision history/rationale rather than canonical project design.

Task/report metadata formats live in `../collaboration/templates/chatgpt-task.md` and `../collaboration/templates/codex-report.md`. Conversation handoff artifacts are governed by `handoff.md`.
