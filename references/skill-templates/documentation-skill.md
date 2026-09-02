# Documentation Skill profile

Use with the common skeleton in `README.md` when the capability is primarily durable
instructions, standards, conventions, or reasoning guidance.

## Recommended source package

```text
<skill-name>/
├── SKILL.md
└── references/           # only when on-demand detail is genuinely needed
```

A standalone maintained first-party source repository additionally uses root
`AGENTS.md` from `../skill-agents-template.md`.

## Profile-specific guidance

- `Workflow` should describe how the Agent inspects context, applies the governing
  rules, and produces a decision/review/artifact.
- Use `references/` for long standards, domain contracts, decision tables, or
  branch-specific examples that should not load every invocation.
- The normal output is guidance, analysis, review, or an edited artifact—not a
  deterministic runtime product merely for symmetry.
- Do not introduce `scripts/`, `tests/`, or a runtime until a real repeatable
  executable operation emerges.

## Typical examples

Coding standards, manuscript guidance, policy interpretation, scientific conventions,
and review rubrics.
