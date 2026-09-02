# Executable Skill profile

Use with the common skeleton in `README.md` when deterministic scripts, commands,
validators, converters, or other repeatable operations materially implement the
capability.

## Recommended source package

```text
<skill-name>/
├── SKILL.md
├── references/           # optional domain/contracts
├── scripts/
├── tests/                # when behavior warrants independent regression protection
└── pyproject.toml        # only if this Skill owns an independent Python runtime
```

A standalone maintained first-party source repository additionally uses root
`AGENTS.md` from `../skill-agents-template.md`.

## Profile-specific guidance

- `Workflow` should validate entry state, invoke the smallest deterministic operation,
  inspect results, and use free-form Agent reasoning only where deterministic logic
  is insufficient.
- `Resources` should name the real scripts and the conditions under which they are
  used. Do not ask the Agent to reimplement deterministic operations in prose.
- `Outputs` should define stable artifacts/state plus diagnostics when applicable.
- `Runtime` should use the parent project's declared runtime when embedded. Create an
  independent `pyproject.toml` only when the Skill itself owns the executable
  dependency/tooling contract.
- `Verification` should protect the executable contract with the smallest relevant
  checks; project/release verification remains outside this profile.
- Do not extract speculative shared abstractions or add scripts without workflow
  consumers.

## Typical examples

Workspace initialization, deterministic converters, parsers, validators, source
normalizers, and repeatable artifact processors.
