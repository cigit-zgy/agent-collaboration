# Skill templates

Use these templates after reading `../skill-package-architecture.md` and choosing the
actual capability profile of the Skill.

Do not combine templates mechanically. Pick the smallest profile that matches the
capability and add optional resources only when they have real consumers.

| Profile | Template | Use when |
|---|---|---|
| Documentation | `documentation-skill.md` | The Skill primarily provides durable instructions, standards, or reasoning guidance. |
| Executable | `executable-skill.md` | The Skill combines Agent guidance with deterministic scripts or commands. |
| Asset-oriented | `asset-oriented-skill.md` | The Skill creates/manipulates artifacts using reusable templates or static assets. |
| Composite/router | `composite-skill.md` | The Skill mainly routes among bounded downstream Skills or workflow branches. |

For a project-level root workflow Skill, use `../project-skill-template.md` instead of
the generic composite template.

## `AGENTS.md` is an ownership decision, not a profile decision

These four templates describe `SKILL.md` capability/workflow profiles. They do not
decide whether the surrounding repository has an `AGENTS.md`.

Apply this separate rule:

```text
standalone maintained FIRST_PARTY Skill repository
→ root AGENTS.md from ../skill-agents-template.md
→ one of the four SKILL.md templates

embedded sub-Skill in a parent project/repository
→ inherit nearest applicable parent AGENTS.md by default
→ one of the four SKILL.md templates

portable Skill distribution bundle
→ AGENTS.md not required
→ SKILL.md + only runtime resources actually needed

THIRD_PARTY Skill
→ preserve upstream structure
```

A Documentation Skill can therefore have a root `AGENTS.md` when it is an independent
first-party source repository, while an Executable or Composite sub-Skill may have no
local `AGENTS.md` because it inherits the parent project constitution.

Common rules for every Skill template:

- `SKILL.md` is required;
- YAML `name` and trigger-oriented `description` are required;
- keep `SKILL.md` operational and compact;
- use progressive disclosure;
- never create empty optional directories;
- do not duplicate repository/project governance from `AGENTS.md`;
- stop rather than invent missing input, authority, or trust state.
