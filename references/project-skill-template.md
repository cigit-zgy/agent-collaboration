# Project workflow `SKILL.md` template

Use this template when a project exposes an Agent-operable multi-stage or composite workflow.
The Skill may live at any project-declared repository-relative path, such as
`<agent-name>/SKILL.md`.

Read `skill-writing-standard.md` first. That reference defines the collaboration-wide writing
principles for every maintained `SKILL.md`.

A project workflow Skill is an operational router, not the project constitution. Root `AGENTS.md`
owns project-level governance. When a project declares canonical design-authority concepts, the
workflow Skill projects that accepted design into an executable route.

## Required information

A project workflow Skill must make the following information easy to recover:

1. workflow purpose and activation condition;
2. minimum project entry state;
3. canonical top-level workflow or branch structure;
4. the owner of each top-level stage/capability;
5. the stable input, output, and progression gate for each route;
6. progressive-disclosure routing to the active downstream Skill/reference;
7. completion semantics for the requested route.

These are information requirements, not mandatory section headings.

## Recommended shape

Use the smallest structure that communicates the real workflow. A common shape is:

```markdown
---
name: <project-skill-name>
description: >
  <WHAT THIS WORKFLOW DOES>. Use when <CONCRETE TRIGGER OR INPUT STATE>.
---

# <Project Skill title>

## Purpose

<One concise statement of the workflow responsibility and stable outcome.>

## Entry state

<Minimum project state required to route correctly.>

## Workflow

```text
<stage_01>
→ <stage_02>
→ <stage_03>
```

## Routing

### `<stage_or_capability_a>`

- Purpose: <ONE-SENTENCE RESPONSIBILITY>.
- Required input: <MINIMUM STABLE INPUT>.
- Stable output: <OUTPUT/STATE>.
- Gate: <DIRECTLY CHECKABLE CONDITION>.
- Owner: `<path/to/sub-skill/SKILL.md>`.

### `<stage_or_capability_b>`

- Purpose: <ONE-SENTENCE RESPONSIBILITY>.
- Required input: <MINIMUM STABLE INPUT>.
- Stable output: <OUTPUT/STATE>.
- Gate: <DIRECTLY CHECKABLE CONDITION>.
- Owner: `<path/to/sub-skill/SKILL.md>`.

## Completion

<Directly checkable terminal state for the requested route.>

## References

<Route only to resources needed by the active branch.>
```

The headings above are examples. Omit or rename sections when the same information is communicated
more clearly another way.

## Route record

For each real top-level route, prefer a compact five-fact record:

```text
purpose
required input
stable output
gate
owner
```

Add another field only when it changes routing or execution.

## Design projection

When the project uses design-authority concepts, identify the governing design topic without copying
it into the Skill.

Example:

```text
Canonical design authority:
reports/concept/<topic>.md

Operational projection:
this SKILL.md + owning downstream Skills/references
```

A project design change is resolved at the design-authority layer first. The workflow Skill then
projects the accepted design.

## Progressive disclosure

Ordinary runtime should follow the shortest valid path:

```text
applicable AGENTS.md
→ project workflow SKILL.md
→ one owning stage Skill
→ only resources required by the active branch
```

Design/redesign/conformance work follows the target project's declared design-authority path before
changing operational projections or implementation.

## Optional topics

Include these only when they are real routing concerns:

- trust/lifecycle state;
- runtime/environment identity;
- branch-specific human checkpoints;
- recovery routing;
- stop conditions.

Detailed scientific schemas, stage-internal algorithms, field semantics, and implementation details
belong to their owning stage Skill/reference rather than the project router.

## Completion and STOP

Define the valid terminal state positively first.

Use STOP only for conditions where the router cannot continue deterministically, such as unresolved
design authority, missing route ownership, unsatisfied upstream gates, or an unauthorized
human/scientific/trust transition.

## Review checklist

A project workflow Skill is ready when:

- an unfamiliar Agent can identify the correct top-level route;
- every route has one clear owner;
- route inputs, outputs, and gates are concrete;
- design authority and operational projection remain distinct;
- normal runtime does not require loading unrelated stages/resources;
- the document does not repeat detailed downstream contracts;
- the structure follows the real workflow rather than a fixed section template.

A project may expose this Skill to Codex under `$REPO_ROOT/.agents/skills/` when repo-scoped
auto-discovery is desired; see `skill-repository-policy.md`. Discovery exposure is separate from the
maintained source location.
