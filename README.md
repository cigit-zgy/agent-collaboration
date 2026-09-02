# agent-collaboration

`agent-collaboration` is a maintained first-party Skill repository that defines the
shared operating model for:

```text
User ↔ ChatGPT ↔ Codex
```

It standardizes how project design, repository maintenance, local execution,
verification, reports, concepts, project onboarding, and Skill packaging are divided
across the three roles without turning every project into a copy of the same
instructions.

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

Responsibilities in this repository:

- `AGENTS.md` — repository-maintenance constitution for Codex-oriented Agent work.
- `SKILL.md` — reusable collaboration workflow/router.
- `references/` — current collaboration/project/Skill operational policy and reusable
  templates.
- `reports/concept/` — this repository's accepted decision history/rationale.
- `reports/chatgpt/` — committed implementation-ready local tasks.
- `reports/codex/` — Codex execution and verification evidence.

## Project design model

Scientific/research projects may use a stronger project-local concept model than this
repository itself.

For maintained water research projects, the default relationship is:

```text
User + ChatGPT discussion/design
        ↓
reports/concept/
canonical project design specification
        ↓
SKILL.md + references/
operational projection
        ↓
scripts / code / schemas
implementation
        ↓
tests/
conformance verification
        ↓
workspace / runtime artifacts
```

This prevents implementation from becoming the accidental source of truth. If a
Skill/reference or code path disagrees with the governing project concept, treat the
difference as projection/implementation drift unless User + ChatGPT explicitly change
the design first.

Project design authority and model-specific scientific fact authority are separate.
For source-grounded modelling, registered original sources and evidence/provenance
remain the authority for values, equations, symbols, and scientific assertions.

## Runtime reading path

Normal project operation remains progressively disclosed:

```text
applicable AGENTS.md
→ project workflow SKILL.md
→ owning sub-Skill
→ only required reference/resource
```

Design/redesign/conformance-audit work instead reads only the relevant canonical
project concept before inspecting or changing its operational projection.

## Project model

The repository provides one responsibility-based architecture for maintained
water-domain research projects, including both mechanistic/dynamic-model projects and
water-domain Agent projects.

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

First-party maintained source normally lives under
`/Users/wenv/Documents/skills/<name>/`. Current Codex discovery uses `.agents/skills`
locations; a user-scoped first-party Skill can normally be exposed through
`$HOME/.agents/skills/<name>` via symlink to the maintained source. External reusable
distribution may use a supported plugin.

## Entry references

Start with the smallest relevant authority:

- collaboration roles and delegation: `references/protocol.md`
- project onboarding and authority model: `references/project-integration.md`
- project architecture: `references/project-architecture.md`
- project `AGENTS.md` scaffold: `references/project-agents-template.md`
- project workflow Skill scaffold: `references/project-skill-template.md`
- concept/report roles: `references/report-concept-policy.md`
- Skill repository/discovery policy: `references/skill-repository-policy.md`
- Skill package architecture: `references/skill-package-architecture.md`
- standalone first-party Skill `AGENTS.md`: `references/skill-agents-template.md`
- Skill capability templates: `references/skill-templates/`
- verification and environment policy: `references/verification-levels.md`,
  `references/verification-tools.md`, `references/skill-environment-policy.md`
- formal tasks/reports: `references/chatgpt-task-template.md`,
  `references/codex-report-template.md`

## Status

The v1 collaboration architecture, authority consolidation, and machine-local Codex
Skill discovery reconciliation have been verified. Project-specific design authority
is now explicitly separated from its operational projection so scientific projects
can keep User + ChatGPT's accepted design as the upstream source of truth without
forcing concept documents into every routine Agent run.
