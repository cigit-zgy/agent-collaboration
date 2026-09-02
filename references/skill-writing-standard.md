# SKILL.md writing standard

This reference defines the collaboration-wide writing standard for maintained `SKILL.md` files.
It governs how a Skill communicates its operational contract to an Agent. It does not define the
scientific or product semantics of any target project; those remain in the owning project design and
contracts.

This is a local collaboration standard derived from current Agent-Skill practice and observed
scientific-agent repositories. It is not presented as a universal external section template.

## 1. Core objective

A `SKILL.md` should let an unfamiliar Agent answer six questions with minimal reading:

1. What capability does this Skill own?
2. When should the Skill be used?
3. What input or upstream state is required?
4. What is the core execution path?
5. What output or completion state means the task is done?
6. Which additional resource should be loaded only when a specific topic requires it?

These are required information categories, not mandatory Markdown headings.

## 2. Writing model

### 2.1 Describe the valid system first

Use positive contracts as the default form.

Preferred:

```text
Exactly one registered source has role `primary`.
Registered archive bytes remain immutable after registration.
```

Avoid defining the capability mainly through repeated prohibitions:

```text
Do not edit...
Do not change...
Do not replace...
Do not infer...
```

A prohibition is appropriate when it protects a real scientific, trust, authorization, or data-loss
boundary that is not already unambiguous from the positive contract.

### 2.2 One rule, one owner, one statement

Every substantive rule has one owning source.

A `SKILL.md` may summarize a governing project concept or reference for execution, but should not
copy the full rule into multiple files. When the detail is owned elsewhere, route to that owner.

Use this hierarchy when applicable:

```text
project concept
= accepted design semantics

SKILL.md
= operational entry and workflow

reference
= bounded detailed contract

code/schema
= implementation

tests
= conformance evidence
```

### 2.3 Prefer concrete, checkable language

Normative statements should identify observable state, artifacts, fields, transitions, or gates.

Preferred:

```text
Every registered path resolves inside `00_archive/`.
```

Weak:

```text
The workflow should be robust and scientifically rigorous.
```

Words such as `robust`, `proper`, `clean`, `safe`, and `rigorous` require a concrete criterion when
they carry normative meaning.

### 2.4 Use normative vocabulary deliberately

Use these terms only when their strength matters:

- `MUST` — required for conformance;
- `SHOULD` — strong default with a legitimate exception path;
- `MAY` — permitted optional behavior;
- `MUST NOT` — prohibited because violating it crosses a real hard boundary.

Ordinary descriptive text does not need normative keywords.

### 2.5 Keep instructions non-duplicative

State an instruction once at the owning level. Do not repeat the same `ask first`, `do not mutate`,
`do not guess`, or similar rule across several sections for emphasis.

If an invariant affects several workflow steps, define it once and make the steps operate under that
invariant.

## 3. Required information

Every maintained `SKILL.md` must communicate the following information, either in frontmatter or
body text.

### Capability purpose and boundary

State the single responsibility and stable outcome of the Skill.

Prefer one concise definition over a long list of non-goals. A boundary can often be expressed as a
handoff:

```text
`init_workspace` ends at registered source readiness.
Source preparation begins in `source_evidence`.
```

### Activation condition

The `description` frontmatter should identify both capability and trigger whenever practical:

```yaml
---
name: <skill-name>
description: >
  <WHAT THE CAPABILITY DOES>. Use when <CONCRETE TRIGGER OR INPUT STATE>.
---
```

If the trigger is already complete and unambiguous in `description`, a separate `When to use`
section is optional.

### Required input or upstream state

State only the minimum information or state required to start the capability correctly.
Detailed schemas belong in their owning references when progressive disclosure is useful.

### Core procedure

Describe the normal successful path with action-oriented steps or an equivalent workflow.

Prefer:

```text
Discover → Confirm → Register → Verify → Report
```

over long explanatory prose.

The procedure should describe outcomes of steps, not internal implementation layout unless that
layout is itself part of the operational contract.

### Completion or output

Define the stable artifact, state, or predicate that proves completion.

A completion gate should be directly inspectable wherever possible:

```text
predicate A
AND predicate B
AND predicate C
```

Do not use vague success labels as a second truth source when success can be derived from actual
artifacts/state.

### Progressive-disclosure routing

Route only to resources needed for specialized details.

```text
SKILL.md
→ one needed reference/script/asset
```

Do not preload every reference, script, test, asset, or project concept during ordinary runtime.

## 4. Optional sections

Sections are added because a capability has a real independent concern, not because every Skill must
look identical.

Common optional topics include:

- source or object roles;
- recovery and idempotency;
- output format;
- tool usage;
- trust-state transitions;
- domain constraints;
- examples;
- stop conditions;
- next-stage routing.

A simple Skill may legitimately contain only:

```text
Purpose
Workflow
Completion
References
```

A composite/router Skill may need routing and branch-specific gates instead.

## 5. Stop conditions

Use a dedicated stop section only when STOP behavior is a meaningful part of the capability.

Good stop conditions are concrete, such as:

- a required human decision is unresolved;
- required authority or upstream state is absent;
- existing durable state conflicts with the requested state;
- continuing would cross a scientific, trust, authorization, or data-loss boundary.

Do not turn routine validation rules into a long prohibition list. Define the valid state first;
reserve STOP for states that genuinely require the Agent to stop rather than continue deterministically.

## 6. Relationship to detailed references

`SKILL.md` is the capability entry and execution router. It should contain the normal path and enough
contract information to select the correct next resource.

Detailed object schemas, field semantics, domain rules, recovery matrices, exact validation logic, and
large examples should move to the owning `references/` document when they are not required on every
run.

The writing standard for `references/*.md` is intentionally separate and is not defined here.

## 7. Size and complexity guidance

There is no fixed line-count conformance rule. Use size as an architecture signal:

- a simple stage Skill should normally remain compact;
- a long Skill should be checked for duplicated rules, embedded reference material, or multiple
  capabilities;
- a new reference should be created only when it owns a real bounded topic and improves progressive
  disclosure.

Do not split content merely to satisfy an arbitrary line limit.

## 8. Review checklist

Before accepting a `SKILL.md`, verify:

- the capability has one clear responsibility;
- the activation condition is discoverable;
- minimum required input/state is explicit;
- the normal path is action-oriented and ordered where order matters;
- completion is concrete and checkable;
- detailed rules have one owner;
- references are loaded progressively;
- positive contracts dominate the prose;
- `MUST NOT` and STOP are limited to real hard boundaries;
- no section exists only for template symmetry;
- the Skill does not silently redefine governing project design.
