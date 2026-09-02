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
- Codex discovery: `~/.codex/skills/<skill-name>` is a symlink to the local
  source of truth; never place a second copy there.
- Identity: folder name = `SKILL.md` name = GitHub repository name = Codex
  discovery name.

Never initialize `/Users/wenv/Documents/skills/` itself as a Git repository.
Each first-party Skill owns only its own repository inside that directory.

## UPSTREAM_REPOSITORY

Preserve upstream Git ownership. Do not create a `cigit-zgy` mirror.

## UPSTREAM_SKILL

Record the upstream repository and pinned commit or tag. Do not create a
`cigit-zgy` repository for the Skill.

## FIRST_PARTY rename contract

A rename is complete only when all of these change together:

1. local folder;
2. `SKILL.md` name;
3. GitHub repository name;
4. Git `origin`;
5. `~/.codex/skills` symlink;
6. `/Users/wenv/Documents/skills/LOCAL_SKILLS.md`.

Do not rely on a GitHub rename redirect. Partial renames are prohibited.

## Automation boundary

Automation may:

- run `git init` inside one first-party Skill folder;
- create its `PRIVATE` GitHub repository;
- set `origin` when no conflicting remote exists;
- create the discovery symlink;
- update `LOCAL_SKILLS.md`.

Automation must not:

- create a public first-party repository;
- fork or mirror upstream without explicit authorization;
- overwrite an existing remote;
- perform a partial rename.

If the target GitHub repository already exists, inspect and safely reuse it;
never overwrite it.
