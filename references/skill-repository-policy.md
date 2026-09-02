# Skill repository policy

Classify every Skill as exactly one of:

- `FIRST_PARTY`
- `THIRD_PARTY`

## FIRST_PARTY

A first-party Skill is designed and maintained by the user.

- Local source root: `/Users/wenv/Documents/skills/<skill-name>/`
- One maintained Skill uses one folder and one user-owned GitHub repository.
- GitHub repository name equals the Skill folder name.
- Repository visibility is `PRIVATE` unless the User explicitly chooses otherwise.
- Identity: folder name = `SKILL.md` `name:` = GitHub repository name.
- `/Users/wenv/Documents/skills/LOCAL_SKILLS.md` records ownership, source,
  repository, purpose, and update strategy.

Do not copy, move, or symlink first-party Skills into `~/.codex/skills/`.
Never initialize `/Users/wenv/Documents/skills/` itself as a Git repository.
Each first-party Skill owns only its own repository inside that directory.

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

## FIRST_PARTY rename contract

A rename is complete only when all of these agree:

1. local folder name;
2. `SKILL.md` `name:`;
3. GitHub repository name;
4. Git `origin`;
5. `/Users/wenv/Documents/skills/LOCAL_SKILLS.md`;
6. active non-historical references to that Skill name in local global routing.

After a GitHub repository rename, explicitly reset `origin`; do not rely on a
GitHub redirect. Partial renames are prohibited.

## Automation boundary

Automation may:

- run `git init` inside one first-party Skill folder;
- create its GitHub repository with the User-approved visibility;
- set `origin` when no conflicting remote exists;
- rename a first-party repository and update its active local references;
- update `LOCAL_SKILLS.md`.

Automation must not:

- publish a private first-party repository publicly without explicit approval;
- fork or mirror third-party content without explicit authorization;
- overwrite an existing remote;
- copy, move, or symlink a first-party Skill into `~/.codex/skills/`;
- perform a partial rename.

If a target GitHub repository already exists, inspect and safely reuse it; never
overwrite it.
