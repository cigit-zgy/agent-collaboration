# Skill repository policy

Classify every Skill as exactly one of:

- `FIRST_PARTY`
- `THIRD_PARTY`

Repository ownership and portable Skill packaging are separate concerns. A Git source
repository may contain maintenance assets that are not part of the installed/runtime
Skill bundle.

## FIRST_PARTY

A first-party Skill is designed and maintained by the user.

- Local source root: `/Users/wenv/Documents/skills/<skill-name>/`
- One maintained standalone Skill uses one folder and one user-owned GitHub
  repository.
- GitHub repository name equals the Skill folder name.
- Repository visibility is `PRIVATE` unless the User explicitly chooses otherwise.
- Identity: folder name = `SKILL.md` `name:` = GitHub repository name.
- `/Users/wenv/Documents/skills/LOCAL_SKILLS.md` records ownership, source,
  repository, purpose, and update strategy.

Do not copy, move, or symlink first-party Skills into `~/.codex/skills/`.
Never initialize `/Users/wenv/Documents/skills/` itself as a Git repository.
Each first-party Skill owns only its own repository inside that directory.

### Maintained standalone first-party Skill repository

A standalone first-party Skill repository that is maintained over time must keep a
root `AGENTS.md` as its repository-maintenance constitution.

`AGENTS.md` is not the Skill runtime workflow. Root `SKILL.md` remains the
Agent-facing capability authority. `AGENTS.md` tells future maintenance Agents how to
understand and change the repository, which files own which concerns, what runtime or
verification authority applies, and what must not be mixed into the Skill.

Use `skill-agents-template.md` when creating or normalizing this file. Do not delete
`AGENTS.md` merely because the Skill is mature.

### Embedded first-party sub-Skill

A sub-Skill embedded inside a larger project/composite repository normally inherits
the nearest applicable parent `AGENTS.md` and should not receive another one merely
for symmetry.

Add a nested `AGENTS.md` only when the subtree has genuine local maintenance rules
that must narrow or override the parent scope.

### Distribution boundary

A portable Skill bundle does not require `AGENTS.md`. A packaging/install process may
ship only:

```text
SKILL.md
references/   # if required
scripts/      # if required
assets/       # if required
```

while the maintained source repository keeps `AGENTS.md`, tests, reports, README,
CI/configuration, or other maintenance assets. Excluding maintenance files from a
runtime bundle is not a reason to delete them from source.

After ownership is established, initialize the Skill from
`skill-package-architecture.md` and the matching purpose-specific template under
`skill-templates/`. Do not create optional directories unless the Skill has a real
consumer for them.

## THIRD_PARTY

A third-party Skill or Skill repository is maintained upstream by another owner.

- Install or discover it through `~/.codex/skills/` or the official Codex plugin
  mechanism.
- When a full upstream repository is needed, keep it under `~/.codex/upstream/`
  and expose only the required Skill through `~/.codex/skills/`.
- Prefer an official Codex plugin when it is reliable and does not create duplicate
  discovery.
- Preserve upstream ownership and record the upstream repository plus pinned commit
  or tag where practical.
- Do not create a `cigit-zgy` mirror merely to consume an upstream Skill.
- Never silently convert third-party content into first-party ownership.

Do not normalize third-party Skill package architecture or inject first-party
`AGENTS.md` conventions merely to match our templates. Preserve upstream layout
unless an explicit adapter is required for consumption.

## FIRST_PARTY rename contract

A rename is complete only when all of these agree:

1. local folder name;
2. `SKILL.md` `name:`;
3. GitHub repository name;
4. Git `origin`;
5. `/Users/wenv/Documents/skills/LOCAL_SKILLS.md`;
6. active non-historical references to that Skill name in local global routing.

After a GitHub repository rename, explicitly reset `origin`; do not rely on a GitHub
redirect. Partial renames are prohibited.

## Automation boundary

Automation may:

- run `git init` inside one first-party Skill folder;
- create its GitHub repository with the User-approved visibility;
- set `origin` when no conflicting remote exists;
- rename a first-party repository and update its active local references;
- update `LOCAL_SKILLS.md`;
- instantiate the approved root `AGENTS.md` and minimal first-party Skill package
  after User + ChatGPT have settled the capability boundary and purpose profile.

Automation must not:

- publish a private first-party repository publicly without explicit approval;
- fork or mirror third-party content without explicit authorization;
- overwrite an existing remote;
- copy, move, or symlink a first-party Skill into `~/.codex/skills/`;
- perform a partial rename;
- add nested `AGENTS.md` files to embedded sub-Skills without genuine local rules;
- create empty `references/`, `scripts/`, `assets/`, or `tests/` directories merely
  because they appear in the canonical architecture;
- create `pyproject.toml` or an independent runtime without a real executable
  consumer.

If a target GitHub repository already exists, inspect and safely reuse it; never
overwrite it.

## Initialization order

For a new standalone first-party Skill:

```text
classify FIRST_PARTY ownership
→ define capability boundary and trigger
→ create root AGENTS.md from skill-agents-template.md
→ choose purpose profile
→ instantiate minimal package architecture
→ write SKILL.md from the matching template
→ add optional references/scripts/assets/tests/runtime only when justified
→ register in LOCAL_SKILLS.md
→ verify discovery and behavior at the level warranted by the Skill
```

For an embedded sub-Skill:

```text
inherit parent AGENTS.md
→ define capability boundary and trigger
→ choose purpose profile
→ write SKILL.md
→ add only justified optional resources
```

Repository ownership, repository-maintenance instructions, and portable package
architecture are distinct concerns. This file owns ownership/placement; the
`skill-agents-template.md` owns the maintained first-party repository constitution
scaffold; `skill-package-architecture.md` owns package/source-layout rules.
