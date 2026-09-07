# Project concept authority and lifecycle

Load this reference for project design authority, adjudication, freeze/reopen, projection, and concept reading routes.

When **authoring or materially rewriting** a concept topic, `SKILL.md` also routes directly to `templates/concept.md`. The authoring template is cold for routine conformance/review.

## Stable report roles

```text
reports/concept/   = current accepted project design, when declared
reports/chatgpt/   = committed FORMAL local-execution specifications
reports/codex/     = FORMAL execution/verification evidence
reports/handoff/   = conversation context only, when used
```

Formal task/report paths remain stable after issue.

## Concept responsibility

When a project declares `reports/concept/` as design authority, each concept topic is the canonical design for one bounded concern after User + ChatGPT adjudication and User acceptance.

The authority chain is:

```text
reports/concept/
→ SKILL.md + references/
→ scripts/code/schemas
→ tests
→ runtime artifacts
```

Downstream artifacts conform to the governing concept. A mismatch is projection/implementation drift unless User + ChatGPT adjudicate and the User accepts a design change first.

Scientific fact authority remains separate:

```text
project design truth   = reports/concept/
model scientific facts = registered source + evidence/provenance
```

A concept defines how the project represents, validates, or operates on scientific information. Model-specific values/equations/symbols/claims remain source-grounded.

Conversation handoffs may summarize design but never become design authority.

## External prior-art gate — hard requirement

Before freezing a concept for a new maintained project, core subsystem, major algorithm/modeling method, major architecture redesign, important trust/provenance mechanism, or substantial framework/tool choice, User + ChatGPT MUST complete the applicable prior-art gate in `prior-art.md`.

The concept records a compact basis containing the search scope, strongest materially relevant candidates, provenance/source coordinates, `REUSE | ADAPT | REFERENCE_ONLY | REJECT` disposition, and the remaining project-specific gap that justifies custom design.

External prior art is evidence, not project authority.

Routine bug fixes, small bounded refactors, and implementation under an unchanged accepted design do not repeat the full gate.

## Review, adjudication, freeze, projection

External review, prior art, Codex output, tests, and existing implementation are evidence; they do not directly redefine the concept.

For gate-triggered design:

```text
problem / design concern
→ prior-art search + candidate inspection
→ reuse/adapt/reference/reject dispositions
→ canonical concept proposal/update
→ adversarial/expert/implementation review
→ findings
→ User + ChatGPT adjudication
→ User decision
   ├── reject change → concept unchanged
   └── accept change → concept updated
→ freeze current concern
→ SKILL/reference projection
→ implementation
→ conformance verification
```

For routine redesign where prior-art is not newly triggered, work may begin at the current canonical concept.

### Adjudication

A proposed change becomes design only after User + ChatGPT review the finding and the User accepts the resulting solution.

When implementation differs from concept:

```text
concept = A
projection/code = B

→ inspect whether B is drift or evidence A should change
→ User + ChatGPT adjudicate
→ User decides whether accepted design changes
→ if A remains accepted, repair B
→ if design changes, update A first then propagate downstream
```

### Freeze

A concern is frozen when:

```text
responsibility/boundary are clear
AND any applicable prior-art gate is complete and recorded
AND current solution is reviewed/adjudicated by User + ChatGPT
AND User accepts the current solution
AND blocking design ambiguities for intended scope are resolved
AND downstream projection can be written without inventing new semantics
```

Freeze means stable enough to project/implement. It does not mean permanent, implementation-complete, or scientifically validated.

`freeze` is a lifecycle condition, not a required metadata enum/state file.

### Reopening

Reopen a frozen concept only when new evidence or a new User requirement materially changes accepted design.

If reopening introduces a new major design concern or substantially changes method/tool choice, repeat the relevant prior-art gate.

```text
new evidence/requirement
→ User + ChatGPT adjudicate
→ User accepts/rejects change
→ update concept first when accepted
→ re-freeze revised scope
→ update Skill/references/code/tests
```

Routine implementation discoveries that do not change design remain downstream implementation work.

## Concept index

`reports/concept/README.md` is the design map. It identifies active design topics and their downstream operational projections. It is not an implementation-status board.

Authoring shape/metadata guidance lives in `templates/concept.md` and is loaded only when creating or materially rewriting concept content.

## Reading routes

Routine execution uses the already-derived operational projection:

```text
AGENTS.md
→ workflow SKILL.md
→ owning stage/reference/script
```

Do not load concepts for every normal operation when the stable projection is sufficient.

### Design/redesign/conformance

```text
AGENTS.md
→ reports/concept/README.md
→ relevant concept topic(s)
→ affected Skill/reference projection
→ implementation/tests as needed
```

### New project / gate-triggered redesign

```text
AGENTS.md
→ current collaboration prior-art route
→ external evidence + strongest implementation precedents
→ relevant concept topic(s)
→ projection
→ implementation/tests
```

### Concept authoring

```text
concept.md
+ templates/concept.md
```

`SKILL.md` names both directly; do not create a mandatory reference chain.

## Collaboration-repository exception

`agent-collaboration` itself is a protocol/Skill repository. Its active policy lives in `references/`; its own `reports/concept/` files are decision history/rationale rather than canonical runtime policy.
