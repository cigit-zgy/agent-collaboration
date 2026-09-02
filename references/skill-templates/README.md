# Skill templates

Use these templates after `../skill-package-architecture.md` and after the capability
boundary/trigger are known.

The profile files define only profile-specific package/resources. Use the common
`SKILL.md` skeleton below instead of repeating the same progressive-disclosure,
completion, stop, and boundary boilerplate in every profile.

## Profiles

| Profile | Template | Use when |
|---|---|---|
| Documentation | `documentation-skill.md` | Durable instructions, standards, conventions, or reasoning guidance are the main capability. |
| Executable | `executable-skill.md` | Deterministic scripts/commands materially implement the capability. |
| Asset-oriented | `asset-oriented-skill.md` | Reusable templates/static assets are central to artifact creation/manipulation. |
| Composite/router | `composite-skill.md` | The Skill routes among bounded downstream Skills or workflow branches. |

For a project-level workflow Skill, use `../project-skill-template.md` instead of the
generic composite profile.

## Common `SKILL.md` skeleton

```markdown
---
name: <skill-name>
description: >
  <WHAT THE CAPABILITY DOES>. Use when <CONCRETE TRIGGER/INPUT>.
---

# <Skill title>

## Role / purpose

<Capability boundary and stable outcome.>

## When to use

Use when:
- <trigger>.

Do not use for:
- <non-goal>.

## Required inputs / state

- `<input>`: <meaning>.

## Workflow

1. <inspect/validate entry state>
2. <perform capability-specific work>
3. <load only resources needed by the active branch>
4. <produce stable output>

## Outputs

- `<output/state>`: <meaning>.

## Resources

<Route only to references/scripts/assets actually needed by this Skill.>

## Completion and stop conditions

Complete when <directly checkable condition>.

Stop rather than infer when required input/authority is missing, no defined route
matches, or continuing would cross a human/trust boundary without authorization.

## Boundaries

- <capability-specific invariant>
- <what this Skill does not own>
```

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

- `SKILL.md` is the capability entry; `AGENTS.md` is repository/project maintenance
  guidance when applicable.
- Keep `description` trigger-oriented.
- Runtime progressive disclosure is `name + description → SKILL.md → only required
  resources`.
- Do not load project concepts by default.
- Do not create empty optional directories.
- Do not add runtime, scripts, tests, or assets without real consumers.
