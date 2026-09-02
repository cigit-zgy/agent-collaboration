# Skill repository and discovery policy

This contract governs Skill ownership, maintained source, discovery, and distribution.

## Ownership classes

Every consumed Skill is either:

- `FIRST_PARTY` — designed and maintained by the User;
- `THIRD_PARTY` — maintained upstream by another owner.

This two-class model is local policy, not a platform requirement.

Ownership and source location are separate concerns. A first-party Skill may be maintained canonically in GitHub without any machine-local checkout.

## Canonical source modes

A maintained Skill declares one canonical source mode:

```text
REMOTE_CANONICAL
= a GitHub repository is the maintained authority; local copies are optional caches

LOCAL_CANONICAL
= an explicitly declared local source is the maintained authority and may be exposed to Agent discovery
```

Do not infer source mode from the presence of a directory on one machine.

### `agent-collaboration`

The `agent-collaboration` Skill is `REMOTE_CANONICAL`:

```text
repository: cigit-zgy/agent-collaboration
canonical transport: GitHub
```

No local installation is required or assumed.

When another project/task needs this Skill, identify it by:

```text
repository + pinned commit SHA + repository-relative path
```

A verified local checkout at the same repository and pinned commit may be used as a read cache. A stale clone or similarly named local Skill is not equivalent authority.

## Discovery

Discovery paths are conveniences, not maintained-source authority.

When a Skill is intentionally installed for Codex discovery, user-scoped or repository-scoped `.agents/skills/` entries may expose it according to the target platform's current rules. Such exposure is optional and must not be treated as proof that the discovered content is current.

Current platform discovery facts should be rechecked against OpenAI documentation when they materially change installation or routing.

## Source, discovery, and distribution

```text
canonical maintained source
= explicitly declared GitHub repository or local source

Agent discovery entry
= optional path exposing the Skill to a host

portable runtime bundle
= SKILL.md + runtime resources required by consumers

external reusable distribution
= supported plugin/package or another explicit distribution artifact
```

## FIRST_PARTY identity

For a standalone first-party Skill, the canonical repository/source identity, `SKILL.md` name, active distribution/discovery references, and current routing references remain aligned.

For a `REMOTE_CANONICAL` Skill, GitHub repository identity and pinned commit/path references are authoritative. Do not require a local folder, symlink, or `LOCAL_SKILLS.md` entry merely for use.

For a `LOCAL_CANONICAL` Skill, any local-source/discovery invariants must be explicitly declared by the owning environment rather than assumed globally.

## THIRD_PARTY

Preserve upstream ownership and structure. Prefer supported upstream distribution; otherwise consume the exact upstream source/version required by the task without converting it into first-party ownership.

## Resolution safety

When a task names a Skill authority:

```text
exact declared source/version resolves
→ use it

exact source/version unavailable
→ BLOCKED or request a corrected authority reference
```

Do not silently substitute an older clone, another Skill, guessed path rename, or semantically similar document.

## Initialization

For a new first-party Skill:

```text
classify ownership
→ choose canonical source mode deliberately
→ define capability boundary + trigger
→ create repository AGENTS.md when the maintained source is a standalone repository
→ choose package shape from package.md
→ write SKILL.md using writing.md
→ add only justified resources
→ expose discovery only when needed
→ verify behavior at the warranted level
```

Embedded project Skills inherit the nearest applicable project `AGENTS.md` unless real local maintenance rules justify a narrower file.

## Automation boundary

Discovery/source automation preserves existing User-owned entries and canonical ownership. Publishing visibility, destructive replacement, ownership conversion, divergent duplicate sources, or changing canonical source mode require explicit authorization rather than being inferred from convenience.
