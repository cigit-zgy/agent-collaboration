# Skill documentation writing standard

This collaboration-wide house standard governs maintained `SKILL.md` files and the Markdown documents under a Skill's `references/` directory. It is derived from current Agent-Skill practice and observed scientific-agent repositories; it is not a universal external section template.

The governing model is:

```text
SKILL.md
= capability entry, normal workflow, completion, and progressive-disclosure routing

references/*.md
= bounded detailed contracts or durable on-demand knowledge
```

## Shared writing principles

### Valid system first

Describe correct state and normal execution as the main prose. Use prohibitions only for real scientific, trust, authorization, security, or data-loss boundaries that are not already unambiguous from the positive contract.

### One concern, one owner, one statement

Every substantive rule has one owning source. A `SKILL.md` or reference may summarize another owner only when the summary is needed for routing or local interpretation; detailed rules remain at their owner.

```text
project concept = accepted design semantics
SKILL.md        = operational entry/workflow
reference       = bounded detailed contract or on-demand knowledge
code/schema     = implementation
tests           = conformance evidence
```

### Concrete and checkable language

Normative text identifies observable artifacts, fields, states, transitions, mappings, or gates. Vague terms such as `robust`, `proper`, `safe`, or `rigorous` require concrete criteria when they carry normative meaning.

### Normative vocabulary

Use `MUST`, `SHOULD`, `MAY`, and `MUST NOT` only when the strength matters. Ordinary explanatory prose needs no normative keyword.

### Non-duplicative instructions

State an instruction once at its owner. Repetition for emphasis increases context cost and can distort Agent behavior.

### Shallow progressive disclosure

Normal loading should remain shallow:

```text
SKILL.md
→ one directly relevant reference
```

A reference may point to another owning reference when the dependency is real, but chains should remain shallow and should not become a substitute for choosing a clear owner.

---

# `SKILL.md`

## Core objective

An unfamiliar Agent should recover six facts with minimal reading:

1. capability purpose/boundary;
2. activation condition;
3. minimum required input/upstream state;
4. core procedure or routing logic;
5. completion/output state;
6. progressive-disclosure route to specialized resources.

These are information categories, not mandatory Markdown headings.

## Required information

The `description` frontmatter should normally carry capability + trigger:

```yaml
---
name: <skill-name>
description: >
  <WHAT THE CAPABILITY DOES>. Use when <CONCRETE TRIGGER OR INPUT STATE>.
---
```

If `description` already communicates activation unambiguously, a separate `When to use` section is optional.

Normal procedure favors action-oriented flow such as:

```text
Discover → Confirm → Register → Verify → Report
```

Completion is preferably a directly inspectable artifact, state, or predicate rather than a second success flag.

## Optional topics

Add a section only for a real independent concern, for example roles, recovery/idempotency, output format, tool use, trust transitions, domain constraints, examples, STOP behavior, or next-stage routing.

A simple Skill may legitimately contain only:

```text
Purpose
Workflow
Completion
References
```

## STOP behavior

Use a dedicated STOP section only when the Agent must stop rather than continue deterministically: unresolved human decision, missing authority/upstream state, conflicting durable state, or a hard scientific/trust/authorization/data-loss boundary.

## Size guidance

No fixed line count is a conformance requirement. Length is an architecture signal: inspect long Skills for duplicated rules, embedded reference material, or multiple capabilities. Split only when the new file owns a real bounded topic and improves progressive disclosure.

## SKILL review

A Skill is ready when capability, trigger, minimum input/state, normal path, completion, and resource routing are clear; detailed rules have one owner; positive contracts dominate; hard negative/STOP rules are limited to genuine boundaries; and governing project design is not redefined.

---

# `references/*.md`

## Purpose

A reference exists to keep specialized detail out of the always-loaded `SKILL.md` while preserving one durable owner for that detail.

Reference count is project-specific. There is no required number of files, no universal body template, and no requirement that references be assigned to a taxonomy.

## Creation gate

Create a new reference only when all of the following are materially true:

1. the topic is not needed on every Skill invocation;
2. the topic is independently coherent and stable enough to have one owner;
3. at least one real workflow or Agent consumer needs the topic;
4. the owner can be described in one sentence without overlapping another reference.

If the topic is short, always needed, or inseparable from the normal workflow, keep it in `SKILL.md` instead.

## Reference boundary

One reference owns one bounded concern. Good examples include source registration, workspace filesystem semantics, unit normalization, object identity, recovery transitions, or symbol normalization.

Avoid miscellaneous containers such as `notes.md`, `misc-rules.md`, `general-guidance.md`, or `extra-details.md` unless the project can state a precise owning concern for them.

## Required information

Every reference should make these items recoverable when applicable:

- what concern it owns;
- the object, state, convention, procedure, or mapping being defined;
- the exact semantics or rules needed by its consumers;
- any validation, transition, exception, ownership, or interface information material to that concern.

These are information categories, not mandatory headings.

## Common organization examples

The following are common ways to organize a reference. They are examples of useful shapes, not reference types that a document must be classified into.

### Object/state contract

Useful when the concern is an object, state, schema, field, role, interface, or filesystem boundary:

```text
Purpose
→ Object / state
→ Required structure
→ Semantics
→ Rules
→ Validation
→ Ownership / interface
```

### Transition/recovery concern

Useful when the concern is recovery, repair, promotion, retry, or another state transition:

```text
Purpose
→ Entry state
→ Transition
→ Outcomes
→ Recovery / escalation
```

A transition table may be clearer than prose.

### Domain/convention concern

Useful for scientific conventions, terminology, normalization, naming, or interpretation guidance:

```text
Scope
→ Definitions
→ Conventions
→ Representative cases
→ Scientific/standards basis when needed
```

A non-workflow reference does not need an artificial completion gate.

### Mapping or decision tables

A mapping table is a presentation form, not a separate document class. Use it inside any reference when the concern is naturally expressed as:

```text
condition → result
input form → normalized form
error class → recovery action
```

## Scientific references

When a reference contains scientific semantics, distinguish project design from model-specific scientific facts:

```text
project concept/reference
= how scientific information is represented, interpreted, validated, or operated on

registered source/evidence
= model-specific values, equations, symbols, and scientific claims
```

A reference may define evidence requirements and interpretation contracts, but it does not invent source-specific scientific facts.

## Examples

Use examples when they materially disambiguate a contract, mapping, edge case, or output shape. Examples illustrate the rule; they do not silently create additional rules.

Large examples belong in a separate reference or asset only when they have a real consumer and improve progressive disclosure.

## Naming and organization

Use descriptive topic names, normally in lowercase kebab-case:

```text
workspace.md
source-registration.md
unit-normalization.md
object-identity.md
recovery.md
```

The `references/` directory already communicates document type, so suffixes such as `-reference`, `-guide`, or `-contract` are unnecessary unless they resolve a real ambiguity.

Keep a stage's references flat by default. Add subdirectories only when a real second-level grouping improves navigation for several related files.

## Cross-reference discipline

A reference links to another reference only when the other file owns a dependency needed to interpret the current topic. Do not restate that dependency in full.

Prefer:

```text
For source-ID semantics, use `source-registration.md`.
```

over copying the complete source-ID contract into multiple files.

Circular ownership between references is invalid: each substantive rule has one direction of authority.

## Size and splitting

No fixed line-count limit defines conformance. Split a reference when it contains multiple independent concerns with different consumers, owners, or change lifecycles.

Do not split one coherent contract merely to make files shorter.

## Reference review

A reference is ready when:

- its owning concern can be stated in one sentence;
- its content is needed by a real consumer;
- it does not duplicate `SKILL.md` or another reference;
- its semantics are concrete enough for correct use or verification;
- its structure follows the content rather than a mandatory template or taxonomy;
- scientific facts remain source-grounded where applicable;
- cross-reference chains remain shallow;
- examples clarify rather than redefine the contract.
