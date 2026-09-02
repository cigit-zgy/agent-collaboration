# Skill package and runtime architecture

This contract defines the internal structure of a reusable Skill and the conditions under which optional resources/runtime exist.

## Boundaries

Keep maintained source, Codex discovery exposure, and portable runtime/distribution distinct. Repository/discovery placement is governed by `repository.md`.

## Minimal package

```text
<skill-name>/
├── SKILL.md              # required capability entry
├── references/           # optional on-demand knowledge/contracts
├── scripts/              # optional deterministic helpers
├── assets/               # optional reusable non-instruction resources
├── tests/                # optional executable verification
├── pyproject.toml        # optional independent Python runtime authority
└── README.md             # optional human orientation
```

Optional resources exist only for real owners and consumers.

## Resource ownership

- `SKILL.md` — capability entry and normal workflow/routing; writing rules are in `writing.md`.
- `references/` — durable on-demand scientific/domain contracts, semantics, standards, decision tables, or branch-specific guidance.
- `scripts/` — deterministic operations that materially improve correctness, repeatability, speed, or token efficiency.
- `assets/` — reusable non-instruction resources such as templates/style/static fixtures.
- `tests/` — regression/conformance checks for executable behavior when warranted.
- `pyproject.toml` — runtime/tooling authority only when the Skill independently owns executable dependencies.
- `README.md` — human-facing installation/orientation/maintenance information.

## Capability profiles

### Documentation

Primary output is durable guidance, analysis, review, or an edited artifact. Typical package is `SKILL.md` plus only the references that improve progressive disclosure. An executable runtime appears only when a real repeatable operation emerges.

### Executable

Deterministic scripts/commands/validators/converters materially implement the capability. Normal flow validates entry state, invokes the smallest deterministic operation, inspects the result, and uses free-form Agent reasoning where deterministic logic is insufficient. Tests protect the executable contract at the smallest relevant scope.

### Asset-oriented

Reusable templates/style/static resources are central. Normal flow selects only relevant assets/references, generates or modifies the artifact, and verifies contractual properties such as structure, rendering, geometry, or formatting.

### Composite/router

The Skill routes among bounded downstream Skills/branches. Each route should expose only purpose, trigger/required input, stable output, gate/next route, and owner. Cross-cutting routing contracts may live in references; branch-specific procedure remains with the branch owner.

## Runtime ownership

```text
documentation-only Skill
→ no runtime

embedded executable Skill
→ use parent project's declared runtime

standalone first-party Skill with independent executable dependencies
→ may own pyproject/runtime

third-party Skill
→ follow upstream runtime model
```

A healthy existing environment is reused for ordinary work. Environment creation/rebuild is justified by execution need, a demonstrably invalid environment, explicit environment-reproducibility testing, or a release gate.

Machine-wide developer tools such as Semgrep, CodeQL, and pip-audit remain separate from project/Skill runtime dependencies; see `../collaboration/verification.md`.

## Boundary test

A Skill boundary is healthy when capability, activation condition, input/state, stable output, completion condition, and supporting resources are each identifiable. Split only when independent triggers/interfaces/validation responsibilities make separate capabilities real.

## Progressive disclosure

```text
name + description
→ SKILL.md
→ only resources needed by the active branch
```

No profile requires a fixed body-section template.
