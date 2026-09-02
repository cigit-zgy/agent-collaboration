# SKILL.md writing standard

This collaboration-wide house standard governs maintained `SKILL.md` files. It is derived from current Agent-Skill practice and observed scientific-agent repositories; it is not a universal external section template.

## Core objective

An unfamiliar Agent should recover six facts with minimal reading:

1. capability purpose/boundary;
2. activation condition;
3. minimum required input/upstream state;
4. core procedure or routing logic;
5. completion/output state;
6. progressive-disclosure route to specialized resources.

These are information categories, not mandatory Markdown headings.

## Writing model

### Valid system first

Describe correct state and normal execution as the main prose. Use prohibitions only for real scientific, trust, authorization, security, or data-loss boundaries that are not already unambiguous from the positive contract.

### One rule, one owner, one statement

A Skill may summarize a governing concept/reference for execution but routes to the owner for detail rather than duplicating the full rule.

```text
project concept = accepted design semantics
SKILL.md        = operational entry/workflow
reference       = bounded detailed contract
code/schema     = implementation
tests           = conformance evidence
```

### Concrete and checkable

Normative text identifies observable artifacts, fields, states, transitions, or gates. Vague terms such as `robust`, `proper`, `safe`, or `rigorous` require concrete criteria when they carry normative meaning.

### Normative vocabulary

Use `MUST`, `SHOULD`, `MAY`, and `MUST NOT` only when the strength matters. Ordinary explanatory prose needs no normative keyword.

### Non-duplicative instructions

State an instruction once at its owner. Repetition for emphasis increases context cost and can distort Agent behavior.

## Required information

The Skill communicates purpose/boundary, activation, minimum entry state, normal procedure, completion/output, and progressive-disclosure routing. The `description` frontmatter should normally carry capability + trigger:

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

Completion is preferably a directly inspectable artifact/state/predicate rather than a second success flag.

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

## Relationship to references

`SKILL.md` is the capability entry and execution router. Detailed schemas, field semantics, domain rules, recovery matrices, exact validation logic, and large examples move to their owning `references/` document when not needed on every run.

The detailed writing standard for `references/*.md` is intentionally left for its own design discussion.

## Size guidance

No fixed line count is a conformance requirement. Length is an architecture signal: inspect long Skills for duplicated rules, embedded reference material, or multiple capabilities. Split only when the new file owns a real bounded topic and improves progressive disclosure.

## Review

A Skill is ready when capability, trigger, minimum input/state, normal path, completion, and resource routing are clear; detailed rules have one owner; positive contracts dominate; hard negative/STOP rules are limited to genuine boundaries; and governing project design is not redefined.
