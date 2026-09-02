# agent-collaboration

`agent-collaboration` is a maintained first-party Skill repository that defines the shared operating model for:

```text
User ↔ ChatGPT ↔ Codex
```

It standardizes how project design, repository maintenance, local execution, verification, reports, concepts, project onboarding, and Skill packaging are divided across the three roles without turning every project into a copy of the same instructions.

## Core logic

```text
User
→ sets goals and makes genuine human decisions

ChatGPT
→ inspects evidence
→ resolves design with the User
→ performs work directly when its connected tools are sufficient
→ delegates only genuinely local/unavailable work
→ independently audits the result

Codex
→ executes committed local tasks
→ preserves local state
→ runs the required verification
→ reports evidence
→ does not silently redesign the task
```

The central authority split is:

```text
User + ChatGPT = design authority
Codex          = local implementation/execution authority
```

## Repository structure

```text
agent-collaboration/
├── AGENTS.md
├── SKILL.md
├── README.md
├── references/
└── reports/
    ├── concept/
    ├── chatgpt/
    └── codex/
```

Responsibilities:

- `AGENTS.md` — repository-maintenance constitution for Codex-oriented Agent work.
- `SKILL.md` — reusable collaboration workflow/router.
- `references/` — current operational authority: protocol, project/Skill architecture, templates, verification, environment, report, and repository policies.
- `reports/concept/` — decision rationale and history; not a competing operational-policy layer.
- `reports/chatgpt/` — committed implementation-ready local tasks.
- `reports/codex/` — Codex execution and verification evidence.

## Runtime reading path

Normal project work should use progressive disclosure:

```text
applicable AGENTS.md
→ project workflow SKILL.md
→ owning sub-Skill
→ only required reference/resource
```

Concept history is read only when a task needs the reason or history behind a durable design decision.

## Project model

The repository provides one responsibility-based architecture for maintained water-domain research projects, including both mechanistic/dynamic-model projects and water-domain Agent projects.

Typical responsibilities are conditional rather than mandatory:

```text
src/          reusable implementation
models/       durable model-specific artifacts
data/         canonical reusable project data
workspace/    mutable working state
experiments/  controlled research investigations
tests/        regression/contract verification
docs/         durable technical documentation
manuscript/   publication assets
```

Only create a responsibility when it has a real owner, artifact, and consumer.

## Skill model

Keep these boundaries separate:

```text
maintained Skill source repository
≠ Codex discovery exposure
≠ portable Skill distribution
```

First-party maintained source normally lives under `/Users/wenv/Documents/skills/<name>/`. Current Codex discovery uses `.agents/skills` locations; a user-scoped first-party Skill can normally be exposed through `$HOME/.agents/skills/<name>` via symlink to the maintained source. External reusable distribution may use a supported plugin.

## Entry references

Start with the smallest relevant authority:

- collaboration roles and delegation: `references/protocol.md`
- project onboarding: `references/project-integration.md`
- project architecture: `references/project-architecture.md`
- project `AGENTS.md` scaffold: `references/project-agents-template.md`
- project workflow Skill scaffold: `references/project-skill-template.md`
- Skill repository/discovery policy: `references/skill-repository-policy.md`
- Skill package architecture: `references/skill-package-architecture.md`
- standalone first-party Skill `AGENTS.md`: `references/skill-agents-template.md`
- Skill capability templates: `references/skill-templates/`
- verification and environment policy: `references/verification-levels.md`, `references/verification-tools.md`, `references/skill-environment-policy.md`
- task/report lifecycle: `references/chatgpt-task-template.md`, `references/codex-report-template.md`, `references/report-concept-policy.md`

## Status

The v1 architecture and GitHub-side policy consolidation are implemented. The remaining release gate is machine-local reconciliation and verification of current Codex Skill discovery/instruction behavior under formal task `reports/chatgpt/260902_chatgpt_05.md`.
