# Composite/router Skill profile

Use with the common skeleton in `README.md` when the Skill primarily routes an Agent
among bounded downstream Skills or workflow branches.

## Recommended source package

```text
<composite-skill>/
├── SKILL.md
├── references/           # only cross-cutting routing contracts
├── <sub-skill-a>/SKILL.md
├── <sub-skill-b>/SKILL.md
└── ...
```

For a project-level workflow Skill, prefer `../project-skill-template.md`. A
standalone maintained first-party source repository additionally uses root
`AGENTS.md` from `../skill-agents-template.md`.

## Profile-specific guidance

- `Workflow` should be a stage sequence or branch decision tree, not downstream
  implementation prose.
- For each route keep only:

```text
purpose
trigger/required input
stable output
gate/next route
owning Skill
```

- Cross-cutting contracts may live in `references/`; branch-specific rules belong to
  the owning sub-Skill.
- Runtime progressive disclosure loads only the selected downstream Skill, then only
  resources needed by that branch.
- Stop when no route matches, an upstream gate fails, a required downstream Skill is
  absent, or a human/trust transition is required.
- Do not create forwarding layers that add no real routing or interface value.

## Typical examples

Multi-stage scientific workflows, capability families, project Agent routers, and
branching automation systems composed of independently bounded sub-Skills.
