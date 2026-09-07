# Project concept authority and lifecycle

Load this reference for project design authority, adjudication, freeze/reopen, projection, and concept reading routes. Report-family layout, filename rules and common metadata are owned by `reports.md`. When authoring or materially rewriting a concept topic, also load `templates/concept.md`.

## Stable report roles

```text
reports/concept/ = current accepted project design, when declared
reports/chatgpt/ = committed FORMAL local-execution specifications
reports/codex/   = FORMAL execution/verification evidence
reports/handoff/ = conversation context only, when used
```

All report artifacts obey the canonical dated family filename and YAML metadata contract in `reports.md`.

## Concept responsibility

When a project declares `reports/concept/` as design authority, each concept artifact is the canonical design for one bounded concern after User + ChatGPT adjudication and User acceptance.

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

Conversation handoffs may summarize design but never become design authority.

## External prior-art gate — hard requirement

Before freezing a concept for a new maintained project, core subsystem, major algorithm/modeling method, major architecture redesign, important trust/provenance mechanism, or substantial framework/tool choice, User + ChatGPT MUST complete the applicable prior-art gate in `prior-art.md`.

The concept records a compact basis containing search scope, strongest materially relevant candidates, source/repository coordinates, `REUSE | ADAPT | REFERENCE_ONLY | REJECT` disposition, and the remaining project-specific gap that justifies custom design. External prior art is evidence, not project authority.

Routine bug fixes, small bounded refactors, and implementation under unchanged accepted design do not repeat the full gate.

## Review, adjudication, freeze, projection

External review, prior art, Codex output, tests, and implementation are evidence; they do not directly redefine the concept.

```text
problem / design concern
→ prior-art gate when applicable
→ canonical concept proposal/update
→ adversarial/expert/implementation review
→ User + ChatGPT adjudication
→ User acceptance/rejection
→ freeze current concern
→ SKILL/reference projection
→ implementation
→ conformance verification
```

When implementation differs from concept, inspect whether implementation drift should be repaired or new evidence justifies reopening design. Accepted design changes are committed to concept first, then propagated to Skill/references/code/tests.

### Freeze

A concern is frozen when responsibility/boundary are clear, any applicable prior-art gate is complete, current solution is adjudicated and accepted, blocking design ambiguities for intended scope are resolved, and downstream projection can be written without inventing semantics.

Freeze means stable enough to project/implement; it does not mean permanent, implementation-complete, or scientifically validated.

### Reopening

Reopen a frozen concept only when new evidence or a new User requirement materially changes accepted design. If reopening introduces a new major method/tool concern, repeat the relevant prior-art gate.

## Concept identity and discovery

Concept files do not use semantic filenames or `README.md` indexes. They use:

```text
reports/concept/YYMMDD_concept_NN.md
```

Each concept carries a stable semantic `concept_id`, title, status, role and summary in YAML metadata. The semantic identity therefore survives filename chronology while repository-wide naming remains uniform.

When a project needs a design map, it is itself a normal concept artifact with a `concept_id` such as `design_map` and the same canonical filename/metadata contract. It may point to active concept topics and downstream operational projections but must not become a parallel implementation-status database.

## Reading routes

Routine execution uses the already-derived operational projection:

```text
AGENTS.md
→ workflow SKILL.md
→ owning stage/reference/script
```

### Design/redesign/conformance

```text
AGENTS.md
→ locate relevant reports/concept artifact by metadata (`concept_id`, title, status)
→ governing concept topic(s)
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

## Roadmap/status boundary

Do not create `reports/development-roadmap.md` or another parallel design/status file. Accepted architectural direction and deferred capabilities that materially constrain future design belong in the owning concept topic. Non-authoritative execution backlog belongs in tasks/issues or another explicitly declared work-management surface.

## Collaboration-repository exception

`agent-collaboration` itself is a protocol/Skill repository. Its active policy lives in `references/`; its own report history does not override runtime policy.
