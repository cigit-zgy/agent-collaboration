# Skill documentation writing standard

Load this reference when authoring or reviewing maintained `SKILL.md` files and their `references/` documentation.

Skill behavior/design lifecycle is owned by `development.md`; source/discovery by `repository.md`; package/resources by `package.md`.

## Governing model

```text
SKILL.md
= capability trigger + runtime entry + core workflow/routing

references/*.md
= bounded specialized contracts/knowledge loaded only when needed

scripts/
= deterministic/repetitive executable work that can often run without loading its implementation into context

assets/
= output resources; not instructional context
```

## Shared principles

### Valid system first

Describe correct state and normal execution as the main prose. Use prohibitions only for real scientific, trust, authorization, security, data-loss, or routing boundaries that are not already unambiguous from the positive contract.

### One concern, one owner, one statement

Every substantive rule has one owning source.

```text
project concept = accepted design semantics
SKILL.md        = operational entry/workflow/routing
reference       = bounded detailed contract/on-demand knowledge
code/schema     = implementation
tests           = conformance/design evidence
```

A router may summarize an owner only enough to select it. Detailed rules remain at the owner.

### Concrete and checkable language

Normative text identifies observable artifacts, fields, states, transitions, mappings, or gates. Vague terms such as `robust`, `proper`, `safe`, or `rigorous` require concrete criteria when they carry normative meaning.

### Normative vocabulary

Use `MUST`, `SHOULD`, `MAY`, and `MUST NOT` only when strength matters. Ordinary explanatory prose needs no normative keyword.

## Progressive disclosure — hard architecture

Maintained Skills use a three-level context model consistent with current Agent-Skill practice:

```text
1. frontmatter metadata
   → always-discoverable trigger surface

2. SKILL.md body
   → loaded when the Skill triggers
   → core workflow + direct routing only

3. bundled resources
   → references/scripts/assets used only when the active branch requires them
```

### Description is the trigger surface

The `description` field must state both capability and when to use it. Do not hide essential activation semantics only in the body.

```yaml
---
name: <skill-name>
description: >
  <WHAT THE CAPABILITY DOES>. Use when <CONCRETE TRIGGER/INPUT STATE>.
---
```

### `SKILL.md` is the runtime index

For a composite Skill, keep selection/routing in `SKILL.md` itself.

Do not add a mandatory second runtime index merely to route from the Skill to its references:

```text
preferred
SKILL.md → owning reference

avoid
SKILL.md → INDEX.md → owning reference
```

A human-facing README or maintenance catalog may exist, but normal Agent execution should not require it.

### Direct read sets

`SKILL.md` should state when each specialized owner is needed.

Normal target:

```text
one primary reference
+ zero or one explicitly necessary secondary reference
```

Do not instruct Agents to preload an entire `references/` directory.

### One-level reference depth

A reference should be substantially self-contained for its owning concern.

Avoid mandatory chains such as:

```text
SKILL.md → reference A → reference B → reference C
```

If two owners are genuinely required for one route, name both directly in `SKILL.md` rather than forcing discovery through a chain.

Cross-links may exist for maintenance/history, but understanding the current owner should not depend on following them.

### Cold paths

Templates, examples, historical reports, large source material, old handoffs, and unrelated variant references are cold unless the active branch explicitly needs them.

Do not make them normal preload requirements.

## Size guidance

Length is an architecture signal, not a parser-enforced conformance quota.

Current maintained Skill ecosystems commonly treat roughly 500 lines as an upper design signal for `SKILL.md`; this collaboration uses a stronger preference for thin routers in composite Skills.

Use these signals:

```text
SKILL.md
→ keep core workflow/routing compact
→ for a composite router, aim substantially below 500 lines
→ if it grows because detailed owner rules accumulate, move those rules to references

reference
→ one bounded concern
→ if it becomes materially longer than ~300 lines, inspect whether:
   a) multiple activation conditions should split; or
   b) one coherent large reference only needs a TOC
```

Do not split one coherent contract solely to hit a line count. Split when consumers, activation conditions, owners, or change lifecycles are genuinely different.

## `SKILL.md` requirements

An unfamiliar Agent should recover with minimal reading:

1. capability purpose/boundary;
2. activation condition;
3. minimum required input/upstream state;
4. core procedure or routing logic;
5. completion/output state;
6. direct route to specialized resources.

These are information categories, not mandatory headings.

Normal procedure favors action-oriented flow such as:

```text
Discover → Confirm → Register → Verify → Report
```

Completion is preferably a directly inspectable artifact/state/predicate rather than a second success flag.

### Optional topics

Add a section only for a real independent concern: roles, recovery/idempotency, output format, tool use, trust transitions, domain constraints, examples, STOP behavior, or next-stage routing.

A simple Skill may legitimately contain only:

```text
Purpose
Workflow
Completion
References
```

### STOP behavior

Use a dedicated STOP section only when the Agent must stop rather than continue deterministically: unresolved human decision, missing authority/upstream state, conflicting durable state, or hard scientific/trust/authorization/data-loss boundary.

## Reference creation gate

Create a new reference only when materially true:

1. the topic is not needed on every Skill invocation;
2. the topic is independently coherent/stable enough to have one owner;
3. at least one real workflow/Agent consumer needs it;
4. the owner can be described in one sentence without overlapping another reference.

If the topic is short, always needed, or inseparable from normal workflow, keep it in `SKILL.md`.

## Reference boundary

One reference owns one bounded concern. Good examples include source registration, workspace semantics, unit normalization, object identity, recovery transitions, external-tool profiles, or symbol normalization.

Avoid miscellaneous containers such as `notes.md`, `misc-rules.md`, or `general-guidance.md` unless a precise owning concern exists.

A reference should make these recoverable when applicable:

```text
what concern it owns
object/state/convention/procedure/mapping defined
exact semantics needed by consumers
validation/transition/exception/ownership/interface information
```

These are information categories, not mandatory headings.

## Common reference shapes

### Object/state contract

```text
Purpose
→ Object/state
→ Required structure
→ Semantics
→ Rules
→ Validation
→ Ownership/interface
```

### Transition/recovery concern

```text
Purpose
→ Entry state
→ Transition
→ Outcomes
→ Recovery/escalation
```

### Domain/convention concern

```text
Scope
→ Definitions
→ Conventions
→ Representative cases
→ scientific/standards basis when needed
```

### Mapping/decision table

Use tables when naturally expressed as:

```text
condition → result
input form → normalized form
error class → recovery action
```

A mapping table is a presentation form, not a separate document class.

## Scripts and deterministic work

Prefer a script over long prose when the task is deterministic/repetitive and executable behavior is clearer than having the model reproduce the procedure token-by-token.

Scripts should not become hidden design authority. Their semantics still conform to the Skill contract, but an Agent may execute a stable script without loading the full implementation into context.

Do not add scripts for one-off ceremony or when a few direct instructions are clearer.

## Scientific references

Distinguish project design from source-specific scientific facts:

```text
project concept/reference
= how scientific information is represented/interpreted/validated/operated on

registered source/evidence
= model-specific values/equations/symbols/scientific claims
```

A reference may define evidence requirements and interpretation contracts; it does not invent source-specific facts.

## Examples

Use examples when they materially disambiguate a contract, mapping, edge case, or output shape. Examples illustrate the rule; they do not silently create additional rules.

Large examples belong in a cold reference/asset only when they have a real consumer and improve progressive disclosure.

## Naming and organization

Use descriptive lowercase kebab-case names:

```text
workspace.md
source-registration.md
unit-normalization.md
object-identity.md
recovery.md
```

The `references/` directory already communicates document type, so suffixes such as `-reference` or `-guide` are unnecessary unless they resolve ambiguity.

Keep references flat by default. Subdirectories are acceptable for real second-level grouping; directory depth is not the same problem as reference-chain depth.

## Review

A Skill/reference architecture is ready when:

```text
description reliably communicates trigger
SKILL.md contains core workflow/direct routing rather than detailed manuals
normal route reaches owner in one reference hop
owner is substantially self-contained
unrelated/cold resources are not preloaded
each substantive rule has one owner
scientific facts remain source-grounded
examples clarify rather than redefine
```

If an Agent must read several large files before discovering the correct owner, classify that as a Skill routing/design defect.
