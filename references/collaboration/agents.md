# AGENTS.md writing standard

This is the collaboration-wide standard for maintained `AGENTS.md` files.

## Purpose

`AGENTS.md` is a scoped constitution and routing document. It establishes durable context that applies across many tasks.

It is distinct from:

```text
SKILL.md                                   capability/workflow execution
references/collaboration/implementation.md implementation/engineering policy
reports/design/                            current accepted project design when used
reports/concept/                           historical design reasoning/input
CURRENT.md                                 current work edge when used
README.md                                  human-facing orientation
CI/tool config                             mechanical enforcement
```

## Core principles

- Scope locally: root rules are repository-wide; nested AGENTS exists only for real subtree-specific differences.
- Keep it concise and durable: identity, authority, ownership, workflow entry, tooling, checkpoints, hard invariants.
- State authority before procedure.
- Describe valid behavior first; reserve hard prohibitions for real risk/trust/data-loss boundaries.
- One rule, one owner, one statement: route to owning artifacts instead of copying manuals.
- Prefer concrete repository-relative paths and stable commands.
- Ground repository-specific claims in actual repository state.
- Remove stale rules when ownership/layout changes.

## Required information categories

A maintained `AGENTS.md` should make easy to recover:

```text
repository/scope identity
authority and precedence
ownership boundaries
workflow/Skill entry
runtime/tooling/verification authority when relevant
implementation-policy route
human/scientific/trust checkpoints
short hard invariants
```

These are information categories, not mandatory headings.

## Recommended shape

````markdown
# <REPOSITORY_OR_SCOPE> context

## Identity
<What this repository/subtree owns.>

## Authority
<Current truth/precedence and design/operation owners.>

## Ownership
```text
<path>  <responsibility>
```

## Workflow
<Primary Skill/entry point and shortest reading route.>

## Runtime and verification
<Stable project-local tooling and routes to global implementation/verification owners.>

## Human / trust checkpoints
<Only genuine decisions/trust transitions.>

## Hard invariants
<Short repository-wide boundaries.>
````

## Layering

```text
user/global instructions
→ repository root AGENTS.md
→ nested AGENTS.md only for real subtree-specific rules
→ SKILL.md / references for capability details
```

For projects using living design, normal current-design routing should point to `reports/design/`, while historical reasoning points to `reports/concept/`.

## Review checklist

An `AGENTS.md` is ready when an unfamiliar Agent can identify scope, authority, owner paths, workflow entry, implementation/runtime/verification authority, and genuine checkpoints without loading unrelated manuals.
