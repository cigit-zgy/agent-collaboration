# Skill templates

Use these templates after `../skill-package-architecture.md` and after the capability boundary and
trigger are known.

Read `../skill-writing-standard.md` first. It defines the collaboration-wide writing standard for all
maintained `SKILL.md` files.

The profile files below define profile-specific package/resources. They do not impose one universal
body-section layout on every Skill.

## Profiles

| Profile | Template | Use when |
|---|---|---|
| Documentation | `documentation-skill.md` | Durable instructions, standards, conventions, or reasoning guidance are the main capability. |
| Executable | `executable-skill.md` | Deterministic scripts/commands materially implement the capability. |
| Asset-oriented | `asset-oriented-skill.md` | Reusable templates/static assets are central to artifact creation/manipulation. |
| Composite/router | `composite-skill.md` | The Skill routes among bounded downstream Skills or workflow branches. |

For a project-level workflow Skill, use `../project-skill-template.md` instead of the generic
composite profile.

## Required `SKILL.md` information

Every maintained Skill must communicate:

```text
capability purpose/boundary
activation condition
minimum required input/state
core procedure or routing logic
completion/output state
progressive-disclosure route
```

These are required information categories, not mandatory Markdown headings.

A simple Skill may use:

```markdown
---
name: <skill-name>
description: >
  <WHAT THE CAPABILITY DOES>. Use when <CONCRETE TRIGGER OR INPUT STATE>.
---

# <Skill title>

## Purpose

<Single responsibility and stable outcome.>

## Workflow

1. <action + result>
2. <action + result>
3. <verify completion>

## Completion

<Directly checkable completion state.>

## References

<Route only to optional resources needed for specialized topics.>
```

An executable Skill may need inputs, outputs, recovery, or tool-use sections. A router may need branch
records and gates. A documentation Skill may need no procedural numbered workflow when another
structure communicates its capability more directly.

## Writing discipline

Use the valid system and normal execution path as the main prose.

Prefer:

```text
Exactly one route owns the active task.
```

over several equivalent negative statements.

Use `MUST NOT` and explicit STOP behavior only for real hard boundaries. Keep detailed object
contracts, large examples, and specialized rules in their owning references when progressive
disclosure improves runtime clarity.

## `AGENTS.md` is an ownership decision

Capability profile does not decide whether a local `AGENTS.md` exists:

```text
standalone maintained FIRST_PARTY source repository
→ root AGENTS.md from ../skill-agents-template.md
→ one capability profile

embedded sub-Skill
→ inherit nearest parent AGENTS.md by default
→ one capability profile

portable distribution
→ AGENTS.md not required

THIRD_PARTY
→ preserve upstream structure
```

## Common rules

- `SKILL.md` is the capability entry; `AGENTS.md` is repository/project maintenance guidance when
  applicable.
- Keep `description` trigger-oriented.
- Runtime progressive disclosure is `name + description → SKILL.md → only required resources`.
- Create optional directories/resources only for real consumers.
- Treat document size as an architecture signal, not a fixed line-count requirement.
- Keep scientific/project semantics in their owning authority rather than redefining them in a Skill.
