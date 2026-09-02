# Maintained first-party Skill repository `AGENTS.md` template

Use this template for a standalone first-party Skill source repository that is
maintained over time. It governs repository maintenance; it is not the portable Skill
runtime contract and is not the Codex discovery location by itself.

Embedded sub-Skills normally inherit the nearest parent/project `AGENTS.md` unless
genuine local maintenance rules require a narrower file.

```markdown
# <SKILL_NAME> repository context

## Repository identity

This repository is the maintained first-party source for the `<SKILL_NAME>` Skill.

<ONE-TO-THREE SENTENCES: capability and repository purpose.>

## Authority

- `AGENTS.md` = repository-maintenance instructions.
- `SKILL.md` = Agent-facing capability/workflow entry.
- `references/` = current Skill-specific operational contracts when present.
- `reports/concept/` = optional decision history/rationale, not runtime policy.

User + ChatGPT own Skill design. Codex executes approved committed local tasks.

## Source / discovery / distribution

```text
maintained source
/Users/wenv/Documents/skills/<skill-name>/

Codex user discovery
$HOME/.agents/skills/<skill-name>
  → normally symlink → maintained source

portable runtime/distribution
SKILL.md + only required runtime resources
```

Do not treat maintained source location as automatic Codex discovery. Do not use
legacy `~/.codex/skills/` as the canonical current discovery contract.

## Repository ownership

```text
SKILL.md        <capability/workflow responsibility>
references/     <if present>
scripts/        <if present>
assets/         <if present>
tests/          <if present>
pyproject.toml  <if present>
README.md       <if present>
reports/        <if this source repository owns collaboration/history assets>
```

Remove lines for nonexistent responsibilities. Do not create paths to satisfy this
template.

## Maintenance rules

- Keep one current operational authority per concern.
- Keep `SKILL.md` compact and progressively disclose branch-specific resources.
- Add deterministic scripts only for real repeatable operations.
- Add tests only for executable behavior that warrants regression protection.
- Do not create an independent runtime when the Skill can correctly use an owning
  project/runtime contract.
- Do not copy maintenance-only artifacts into a portable runtime bundle.

## Runtime and verification

<STATE WHETHER THE SKILL OWNS AN INDEPENDENT RUNTIME.>

Examples:

`No independent runtime; documentation-only Skill.`

or:

```text
Runtime authority: pyproject.toml
Environment: <name>
```

## Hard boundaries

- `AGENTS.md` persists while this source repository is maintained; maturity is not a
  reason to delete it.
- `SKILL.md` governs capability operation; `AGENTS.md` does not duplicate it.
- Codex discovery exposure is separate from maintained source.
- Embedded sub-Skills do not get redundant `AGENTS.md` files by default.
- Third-party Skills keep upstream ownership/layout.
- Optional package resources require real consumers.
```

Do not use this template for a portable bundle, an embedded sub-Skill with no special
maintenance rules, a third-party Skill, or a full scientific/software project.
