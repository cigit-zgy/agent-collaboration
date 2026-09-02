# Skill templates

Use these templates after reading `../skill-package-architecture.md` and choosing the
actual purpose profile of the Skill.

Do not combine templates mechanically. Pick the smallest profile that matches the
capability and add optional directories only when they have real consumers.

| Profile | Template | Use when |
|---|---|---|
| Documentation | `documentation-skill.md` | The Skill primarily provides durable instructions, standards, or reasoning guidance. |
| Executable | `executable-skill.md` | The Skill combines Agent guidance with deterministic scripts or commands. |
| Asset-oriented | `asset-oriented-skill.md` | The Skill creates/manipulates artifacts using reusable templates or static assets. |
| Composite/router | `composite-skill.md` | The Skill mainly routes among bounded downstream Skills or workflow branches. |

For a project-level root workflow Skill, use `../project-skill-template.md` instead of
the generic composite template.

Common rules for every template:

- `SKILL.md` is required;
- YAML `name` and trigger-oriented `description` are required;
- keep `SKILL.md` operational and compact;
- use progressive disclosure;
- never create empty optional directories;
- do not duplicate project governance from `AGENTS.md`;
- stop rather than invent missing input, authority, or trust state.
