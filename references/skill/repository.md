# Skill repository and discovery policy

This contract governs Skill ownership, maintained source, Codex local discovery, and external distribution.

## Ownership classes

Every consumed Skill is either:

- `FIRST_PARTY` — designed and maintained by the User;
- `THIRD_PARTY` — maintained upstream by another owner.

This two-class model is local policy, not a platform requirement.

## Maintained source and discovery

Standalone first-party source is maintained under:

```text
/Users/wenv/Documents/skills/<skill-name>/
```

Codex user-scoped discovery normally exposes it through:

```text
$HOME/.agents/skills/<skill-name>
→ symlink → maintained source
```

Repository-scoped discovery may use:

```text
$REPO_ROOT/.agents/skills/<skill-name>
```

Current platform discovery facts should be rechecked against OpenAI documentation when they materially change installation or routing.

## Source, discovery, and distribution

```text
maintained source repository
= AGENTS.md + SKILL.md + justified maintenance/runtime resources

Codex discovery entry
= .agents/skills path exposing the Skill

portable runtime bundle
= SKILL.md + runtime resources required by consumers

external reusable distribution
= supported plugin/package or another explicit distribution artifact
```

## FIRST_PARTY identity

For a standalone first-party Skill, maintained folder name, `SKILL.md` name, GitHub repository name, Git remote, `LOCAL_SKILLS.md`, active discovery path, and active routing references remain aligned. A rename updates all applicable identities as one operation.

## THIRD_PARTY

Preserve upstream ownership and structure. Prefer supported upstream distribution; otherwise expose the upstream source through the appropriate discovery path without converting it into first-party ownership.

## Initialization

```text
classify ownership
→ define capability boundary + trigger
→ create repository AGENTS.md from templates/agents.md when standalone first-party
→ choose package shape from package.md
→ write SKILL.md using writing.md
→ add only justified resources
→ register maintained source in LOCAL_SKILLS.md
→ expose discovery only when needed
→ verify behavior at the warranted level
```

Embedded project Skills inherit the nearest applicable project `AGENTS.md` unless real local maintenance rules justify a narrower file.

## Automation boundary

Discovery automation preserves existing User-owned entries and source ownership. Publishing visibility, destructive replacement, ownership conversion, or divergent duplicate source copies require explicit authorization rather than being inferred from discovery needs.
