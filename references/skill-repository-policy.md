# Skill repository policy

Classify every maintained Skill as exactly one of:

- `FIRST_PARTY`
- `UPSTREAM_REPOSITORY`
- `UPSTREAM_SKILL`

## FIRST_PARTY

One maintained Skill uses one folder and one private GitHub repository.

- Local source of truth: `/Users/wenv/Documents/skills/<skill-name>/`
- GitHub repository: `cigit-zgy/<skill-name>`
- Repository visibility: `PRIVATE`
- Identity: folder name = `SKILL.md` name = GitHub repository name.
- Index: `LOCAL_SKILLS.md` records ownership, source, repository, purpose, and
  update strategy.

Do not copy, move, or symlink first-party Skills into `~/.codex/skills/`.

Never initialize `/Users/wenv/Documents/skills/` itself as a Git repository.
Each first-party Skill owns only its own repository inside that directory.

## UPSTREAM_REPOSITORY and UPSTREAM_SKILL

Install or discover third-party Skills through `~/.codex/skills/` or the
official Codex plugin mechanism. Prefer an official plugin when available.

Preserve upstream ownership, record the upstream repository and pinned commit
or tag, and do not create a `cigit-zgy` mirror. Never silently turn upstream
content into a first-party fork.

## FIRST_PARTY rename contract

A rename is complete only when all of these change together:

1. local folder;
2. `SKILL.md` name;
3. GitHub repository name;
4. Git `origin`;
5. `/Users/wenv/Documents/skills/LOCAL_SKILLS.md`.

Do not rely on a GitHub rename redirect. Partial renames are prohibited.

## Automation boundary

Automation may:

- run `git init` inside one first-party Skill folder;
- create its `PRIVATE` GitHub repository;
- set `origin` when no conflicting remote exists;
- update `LOCAL_SKILLS.md`.

Automation must not:

- create a public first-party repository;
- fork or mirror upstream without explicit authorization;
- overwrite an existing remote;
- copy, move, or symlink a first-party Skill into `~/.codex/skills/`;
- perform a partial rename.

If the target GitHub repository already exists, inspect and safely reuse it;
never overwrite it.
