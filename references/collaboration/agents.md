# AGENTS.md writing standard

This is the collaboration-wide house standard for maintained `AGENTS.md` files. It is informed by current Codex/AGENTS practice, Anthropic project-instruction guidance, and observed scientific-agent repositories; it is not presented as a universal external section template.

`AGENTS.md` is Codex-oriented in this collaboration standard. Anthropic guidance is used only as evidence for general instruction-writing principles; Claude Code's native project-instruction mechanism is separate and should not be conflated with `AGENTS.md` discovery.

## Purpose

`AGENTS.md` is a scoped constitution and routing document for an Agent working in a repository or directory subtree. It establishes durable context that applies across many tasks.

It is distinct from:

```text
SKILL.md                                  capability/workflow execution
references/collaboration/implementation.md AI-assisted implementation/engineering policy
other references/                         bounded detailed contracts
reports/concept                           accepted project design when declared
README.md                                 human-facing orientation
CI/tool config                            mechanical formatting/lint/build enforcement
```

## Core principles

### Scope locally

A root `AGENTS.md` states repository-wide context. A nested `AGENTS.md` exists only when a subtree has real local instructions that differ from or refine the parent scope. More specific instructions override broader ones for their subtree.

### Keep it concise and durable

Include rules likely to remain relevant across tasks: identity, authority, ownership, workflow entry, runtime authority, trust/human checkpoints, and hard invariants. Task-specific plans, temporary state, implementation history, and one-off debugging notes belong elsewhere.

### State authority before procedure

An unfamiliar Agent should quickly know which files own design, scientific facts, operational workflow, implementation policy, implementation, tests, and mutable state. Routing depends on that precedence.

### Describe the valid behavior first

Use positive contracts as the default. Reserve `MUST NOT` or explicit prohibitions for genuine scientific, trust, authorization, security, or data-loss boundaries. When a dangerous path is named, state the correct path or escalation route when useful.

### One rule, one owner, one statement

Do not duplicate a workflow manual, design specification, coding/implementation standard, global collaboration policy, or installation profile inside `AGENTS.md`. Point to the owning artifact.

### Prefer concrete instructions

Use exact repository-relative paths, owners, commands, gates, and states when they are truly scope-local. Mechanical formatting/lint requirements should normally be enforced by tooling/CI rather than expanded into prose.

### Inspect before claiming

Repository-specific claims should be grounded in the actual repository. Stable commands may be listed when they are genuinely standard for the scope.

### Maintain the file

Stale rules are removed or updated when the repository changes. A longer `AGENTS.md` is not more authoritative; relevance and precedence matter more than volume.

## Required information categories

A maintained `AGENTS.md` should make the applicable items easy to recover:

1. repository/directory identity and scope;
2. authority and precedence;
3. ownership boundaries that affect Agent behavior;
4. workflow/Skill entry and reading route;
5. runtime/tooling/verification authority when relevant;
6. implementation-policy route when code is produced;
7. human/scientific/trust checkpoints when relevant;
8. a short set of real hard invariants or escalation conditions.

These are information categories, not mandatory headings.

## Recommended shape

````markdown
# <REPOSITORY_OR_SCOPE> context

## Identity

<What this repository or subtree owns.>

## Authority

<Current truth/precedence and who owns design/operation.>

## Ownership

```text
<path>  <responsibility>
```

## Workflow

<Primary Skill/entry point and shortest normal reading route.>

## Runtime and verification

<Runtime/tooling authority and stable common commands, only when real. Route AI-assisted implementation to the collaboration implementation contract rather than duplicating it.>

## Human / trust checkpoints

<Only genuine decisions or trust transitions. Human decision authority does not imply human code authorship.>

## Hard invariants

<Short list of repository-wide hard boundaries.>
````

Omit or rename sections when the same required information is communicated more clearly another way.

## Layering

```text
user/global instructions
→ repository root AGENTS.md
→ nested AGENTS.md only for real subtree-specific rules
→ SKILL.md / references for capability and implementation details
```

Repository `AGENTS.md` should route to the nearest owner instead of copying that owner's content.

## Evidence basis

The standard draws on recurring practices from OpenAI Codex, OpenAI model guidance, Anthropic project-instruction guidance, and scientific-agent repositories reviewed for this collaboration. The common pattern is concise scope-local context, clear authority, concrete routing, progressive disclosure, and separation of prompts/configuration/logs rather than one monolithic instruction file.

Platform-specific discovery and precedence facts should be rechecked against current vendor documentation when they materially affect routing.

## Review checklist

An `AGENTS.md` is ready when an unfamiliar Agent can identify the applicable scope, authority, owner paths, workflow entry, implementation/runtime/verification authority, and any genuine human/trust boundary without loading unrelated manuals or installation-specific detail owned elsewhere.
