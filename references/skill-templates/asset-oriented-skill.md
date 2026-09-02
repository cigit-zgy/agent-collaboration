# Asset-oriented Skill profile

Use with the common skeleton in `README.md` when reusable templates, style files,
static resources, or artifact-generation assets are central to the capability.

## Recommended source package

```text
<skill-name>/
├── SKILL.md
├── references/           # optional guidance/contracts
├── scripts/              # optional deterministic helpers
└── assets/
```

Add tests/runtime only when actual executable behavior warrants them. A standalone
maintained first-party source repository additionally uses root `AGENTS.md` from
`../skill-agents-template.md`.

## Profile-specific guidance

- `Workflow` should inspect the requested artifact/constraints, choose only the
  relevant assets/references, generate or modify the artifact, and verify properties
  that matter to the contract.
- `Resources` should route to specific assets and deterministic helpers by condition;
  do not preload every template/style/example.
- Explanatory Markdown belongs in `references/`, not `assets/`.
- `Outputs` should name the stable artifact type/path and any required derivative.
- Verification may cover structure, rendering, geometry, formatting, required
  content, or deterministic reproducibility when those properties are contractual.
- Do not add scripts/tests merely because another asset Skill has them.

## Typical examples

Scientific figures, diagram generation, document templates, slide/document artifact
production, and style-driven rendering workflows.
