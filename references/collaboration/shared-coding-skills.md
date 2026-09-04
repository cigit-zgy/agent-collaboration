# Shared coding Skill authority and alignment

This contract ensures that ChatGPT and Codex use the same applicable coding-Skill instructions when they author, review, verify, or repair code in one collaboration task.

## Core invariant

For every coding Skill that materially constrains a task, both Agents use the same:

```text
Skill identity
+ canonical source
+ immutable revision
+ repository-relative Skill path
+ selected mode/profile when applicable
```

A local discovery path proves only that a host can find some Skill content. It does not prove that the content is the same revision ChatGPT used.

## Precedence

```text
explicit User decision
→ project AGENTS / accepted project design / project tooling
→ project-specific shared coding-Skill profile
→ collaboration shared coding-Skill profile
→ local-only helper Skill
```

A generic coding Skill never overrides an explicit scientific, product, security, data-loss, reproducibility, public-contract, or trust-boundary requirement.

## Authority coordinates

The preferred cross-Agent authority is:

```text
<OWNER>/<REPOSITORY>@<COMMIT>:<PATH/TO/SKILL.md>
```

The commit must be immutable. A branch name such as `main`, a local filesystem path, or a Skill name alone is insufficient for task-level alignment.

A plugin may serve as shared authority only when ChatGPT and Codex can both resolve the same plugin identity, version, and Skill content. Otherwise the plugin is a local execution aid rather than a cross-Agent normative source.

Do not copy third-party Skill bodies into this repository merely to align them. Store only authority coordinates, activation rules, and any approved mode.

## Current collaboration-wide coding profile

These entries are the global cross-Agent defaults at the collaboration revision that contains this file:

| Skill | Immutable authority | Activation | Mode / boundary |
|---|---|---|---|
| `ponytail` | `DietrichGebert/ponytail@2ed6c52c9d7e5e56942508591085fd45dea277d3:skills/ponytail/SKILL.md` | Code design, authoring, fixing, refactoring, and review | `full`; subordinate to explicit scientific/product/security/data-loss/reproducibility/trust requirements |
| `modern-python` | `trailofbits/skills@d3323cefbcf645678b8dc481de204b02ad3d02dc:plugins/modern-python/skills/modern-python/SKILL.md` | New Python projects, Python tooling setup, or an explicitly approved modernization/migration | Conditional; never migrate an existing project merely because this Skill is available |

A locally installed third-party Skill that is absent from this table and absent from a project/task-specific profile may still assist Codex locally, but it does not constrain ChatGPT-authored code until an exact shared authority is registered.

## Project- and task-specific Skills

A project may declare additional shared coding Skills in its root `AGENTS.md` or one project-owned reference. Use the same immutable-coordinate form and state the activation condition and precedence.

A FORMAL task records:

```text
shared coding profile coordinate
activated Skill names/modes
any project/task-specific immutable Skill coordinates
```

The task must not rely on `/Users/...`, `$HOME/.agents/skills/...`, plugin display names, or `LOCAL_SKILLS.md` as the only authority visible to ChatGPT.

## ChatGPT authoring gate

Before ChatGPT writes or reviews code, it:

1. reads the applicable project `AGENTS.md`, accepted design, and project tooling authority;
2. resolves this shared profile at the collaboration commit governing the work;
3. resolves any project/task-specific immutable Skill authorities;
4. reads only the coding Skills activated by the current task;
5. applies those rules while authoring the implementation and tests;
6. records the activated Skills and remaining local verification in the task when a Codex handoff is needed.

ChatGPT must not claim to follow a local-only Skill whose actual content it cannot resolve.

## Codex alignment gate

Before Codex authors, verifies, or repairs code for LOCAL-QUICK or FORMAL work, it compares each activated shared Skill with the local discovered/cached content.

```text
exact identity + revision + path match
→ local copy may be used

mismatch, but exact pinned source is directly readable
→ use the pinned source as authority; local discovery does not override it

local scripts/assets are required and a clean cache can be aligned safely
→ fetch/check out the exact pinned revision and verify it

missing authority, dirty/conflicting local source, or unverifiable plugin version
→ report the mismatch; do not silently use a different revision
```

Alignment is scoped to Skills activated by the task. Do not scan, update, or reinstall every Skill on every invocation.

Codex records the exact authorities actually used and any alignment action in its execution evidence.

## Update policy

Task start performs a cheap identity check, not an automatic update to upstream latest.

Synchronize local content only when:

- the task's pinned shared profile differs from the verified local revision;
- the selected project/task Skill authority changed; or
- the User explicitly requests an upstream update review.

Upstream changes are adopted by reviewing the Skill diff, updating the shared profile deliberately, and using the new collaboration/project revision in future tasks. A running task remains bound to its pinned profile.

This separates two operations:

```text
task alignment
= make both Agents use the task-pinned Skill revision

upstream refresh
= decide whether a newer third-party Skill revision should become the next shared profile
```

Do not combine them implicitly.

## Local inventory boundary

`/Users/wenv/Documents/skills/LOCAL_SKILLS.md` may record machine-local source, discovery path, upstream, and revision. It is useful evidence for reconciliation, but it is not directly available to ChatGPT and therefore cannot be the sole cross-Agent authority.

The remote shared profile is the small normative subset. The local inventory remains the complete machine inventory. Do not create another full duplicate registry.

## Completion

Shared-Skill alignment is complete when every activated cross-Agent coding Skill is resolved to the task-pinned immutable authority by both ChatGPT and Codex, and remaining local-only helper Skills are not allowed to redefine the shared coding contract.