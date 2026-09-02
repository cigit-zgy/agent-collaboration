# Skill repository and discovery policy

This file is the current operational authority for Skill ownership, maintained source,
Codex local discovery, and external distribution.

## Ownership classes

Classify every consumed Skill as exactly one of:

- `FIRST_PARTY`: designed and maintained by the User;
- `THIRD_PARTY`: maintained upstream by another owner.

This two-class ownership model is this repository's policy; it is not an OpenAI
platform requirement.

## Current Codex discovery facts

OpenAI's current Codex documentation defines local Skill discovery under
`.agents/skills` locations:

```text
repository-scoped: $CWD/.agents/skills and parent .agents/skills up to $REPO_ROOT
user-scoped:       $HOME/.agents/skills
admin-scoped:      /etc/codex/skills
system-scoped:     bundled by OpenAI
```

Codex follows symlinked Skill folders. These locations are for authoring/local
discovery. For reusable distribution beyond one repository/user, OpenAI recommends
plugins.

Canonical platform reference:
`https://developers.openai.com/codex/skills`

Do not treat legacy `~/.codex/skills/` as the current canonical discovery contract.

## Host compatibility boundary

The `AGENTS.md` rules in this repository are Codex-oriented project/repository
instructions. They are not claimed to be an Anthropic Claude Code discovery standard
or a universal Agent-host requirement.

Other Agent hosts may use different instruction files or discovery mechanisms. If a
project later targets another host, add an explicit adapter/import/symlink only when
that host is actually supported; do not duplicate all current policy into parallel
files pre-emptively.

The portable `SKILL.md` capability boundary is intentionally more host-neutral than
repository-maintenance `AGENTS.md`, but host-specific Skill discovery/distribution
still follows the target platform's current rules.

## FIRST_PARTY maintained source

A standalone first-party Skill source repository is maintained under:

```text
/Users/wenv/Documents/skills/<skill-name>/
```

Rules:

- one maintained Skill uses one folder and one User-owned GitHub repository;
- folder name = `SKILL.md` `name:` = GitHub repository name;
- repository visibility is `PRIVATE` unless the User explicitly chooses otherwise;
- root `AGENTS.md` is retained as the source-repository maintenance constitution;
- `/Users/wenv/Documents/skills/LOCAL_SKILLS.md` records ownership, source,
  repository, purpose, discovery exposure, and update strategy;
- `/Users/wenv/Documents/skills/` itself is not a Git repository and is not assumed
  to be a Codex discovery location.

### User-scoped Codex discovery bridge

When a standalone first-party Skill should be available to Codex across repositories,
expose the maintained source through:

```text
$HOME/.agents/skills/<skill-name>
  → symlink → /Users/wenv/Documents/skills/<skill-name>
```

Prefer a symlink so maintained source remains single-copy. Before creating or
replacing a discovery path, inspect existing files/symlinks and preserve User work.
Do not overwrite a conflicting discovery entry silently.

### Repo-scoped discovery

A project-owned or embedded Skill that should be discoverable only inside one
repository may be exposed under:

```text
$REPO_ROOT/.agents/skills/<skill-name>
```

The discovered entry may be the maintained Skill folder itself or a repository-local
symlink to the actual package, provided the target is stable and portable for that
repository. A project may also route explicitly to an internal `SKILL.md` from its
`AGENTS.md`; auto-discovery is not required for every internal workflow document.

## THIRD_PARTY Skills

Preserve upstream ownership and prefer current supported distribution/discovery:

1. use an official OpenAI plugin when the upstream Skill is distributed that way and
   doing so does not create duplicate discovery;
2. otherwise keep upstream source in an appropriate upstream location and expose the
   required Skill through `$HOME/.agents/skills/` or repository `.agents/skills/`;
3. symlink rather than mirror when a single upstream source should remain canonical;
4. record upstream repository and pinned tag/commit when practical.

Do not create a `cigit-zgy` mirror merely to consume third-party content. Do not
silently convert third-party content into first-party ownership.

## Source repository versus portable distribution

Keep these separate:

```text
maintained source repository
= AGENTS.md + SKILL.md + justified source/maintenance assets

Codex local discovery entry
= .agents/skills path exposing the Skill to Codex

portable Skill distribution
= SKILL.md + only runtime resources needed by the consumer

external reusable distribution
= plugin or another explicit supported package
```

A source repository can contain reports, tests, CI, maintenance docs, or other assets
that do not belong in the portable runtime bundle.

## FIRST_PARTY rename contract

A standalone first-party rename is complete only when all applicable identities agree:

1. maintained source folder name;
2. `SKILL.md` `name:`;
3. GitHub repository name;
4. Git `origin`;
5. `LOCAL_SKILLS.md`;
6. active discovery symlink/path under `$HOME/.agents/skills/` when present;
7. active non-historical routing references.

After a GitHub repository rename, explicitly reset `origin`. Do not rely on GitHub
redirects. Partial renames are prohibited.

## Initialization order

For a new standalone first-party Skill:

```text
classify FIRST_PARTY
→ define capability boundary and trigger
→ create source-repository AGENTS.md from skill-agents-template.md
→ choose package profile from skill-package-architecture.md
→ write SKILL.md from the matching template
→ add optional resources only when justified
→ register maintained source in LOCAL_SKILLS.md
→ expose through $HOME/.agents/skills only when Codex user-scoped discovery is desired
→ verify discovery and behavior at the warranted level
```

For an embedded project Skill, inherit the nearest applicable project `AGENTS.md` by
default and use repo-scoped `.agents/skills/` only when auto-discovery is desired.

## Automation boundary

Automation may create/update discovery symlinks after inspecting the target and
confirming there is no conflicting User-owned entry. It must not:

- overwrite existing remotes or discovery entries;
- publish private source publicly without explicit approval;
- create duplicate first-party source copies merely for discovery;
- normalize third-party source layout to first-party conventions;
- create empty optional package directories or unnecessary runtimes.
