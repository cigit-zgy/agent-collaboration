---
name: agent-collaboration
description: >
  Coordinate User, ChatGPT, and Codex for repository work that needs design,
  direct remote action, committed local execution, verification, independent audit,
  project onboarding, Skill onboarding, or maintained Skill authoring.
---

# Agent Collaboration

## Role

This Skill is the top-level collaboration router for:

```text
User ↔ ChatGPT ↔ Codex
```

It decides which collaboration contract to load. Detailed operational rules live in
`references/`; this file does not duplicate them.

## Core route

Use `references/protocol.md` when repository work needs the three-party design,
delegation, execution, verification, or acceptance loop.

Key role split:

```text
User + ChatGPT
= design and acceptance

ChatGPT
= direct executor when connected tools are sufficient

Codex
= local executor only when a genuinely local/unavailable capability is required
```

Evidence, not Codex self-reported PASS, determines final acceptance.

## Routing table

- Project onboarding or project-entry normalization:
  `references/project-integration.md` → `references/project-architecture.md` →
  `references/project-agents-template.md`; add a project workflow Skill from
  `references/project-skill-template.md` only when the project exposes an
  Agent-operable workflow.
- Maintained `SKILL.md` authoring or review:
  `references/skill-writing-standard.md` first; then use the relevant project or
  standalone Skill template. The standard defines required information and writing
  discipline without imposing one universal body-section layout.
- Project concept/design authority and report lifecycle:
  `references/report-concept-policy.md`. Scientific/research projects may declare
  selected concepts as canonical design specifications; Skills/references then act as
  operational projections.
- Standalone first-party Skill repository onboarding:
  `references/skill-repository-policy.md` → `references/skill-agents-template.md` →
  `references/skill-package-architecture.md` → `references/skill-writing-standard.md`
  → the appropriate template under `references/skill-templates/`.
- Formal Codex task authoring: `references/chatgpt-task-template.md` plus the
  selected level from `references/verification-levels.md`.
- Codex launch: `references/codex-launch-template.md`.
- Codex execution report: `references/codex-report-template.md`.
- Verification-tool selection: `references/verification-tools.md`.
- Skill/project environment ownership: `references/skill-environment-policy.md`.

## Progressive disclosure

For ordinary collaboration/runtime work, load only the active route:

```text
applicable AGENTS.md
→ this SKILL.md
→ one owning collaboration reference
→ target project workflow SKILL.md when relevant
→ owning sub-Skill
→ only resources required by that Skill
```

Do not preload project concepts during routine operation merely because they exist.

For design/redesign/conformance-audit work, follow the target project's declared
authority model. If selected project concepts are canonical design authority, read the
concept index and only the governing topic(s) before changing their Skill/reference
projection or implementation.

This repository's own concepts remain decision history/rationale; they do not override
`references/*`.

## Project design boundary

Keep these levels distinct when a scientific/research project declares
design-authority concepts:

```text
project concept
= canonical WHAT + WHY + accepted scientific/architectural design

project Skill/reference
= operational projection

code/schema
= implementation

tests
= conformance verification

workspace/source evidence
= runtime artifacts and, where declared, model-specific scientific fact authority
```

If a downstream projection or implementation disagrees with the governing design,
treat it as drift rather than silently changing the design. A design change belongs
to User + ChatGPT first.

## Skill discovery boundary

Maintained source under `/Users/wenv/Documents/skills/` is not itself the canonical
Codex discovery location. Current Codex local discovery uses `.agents/skills`
locations; reusable external distribution should use the platform's supported plugin
or another explicit distribution artifact. The authoritative local policy is
`references/skill-repository-policy.md`.

## Stop conditions

Stop and surface the issue instead of improvising when:

- a design-affecting decision remains unresolved;
- a governing project concept and its operational projection are contradictory;
- the required local capability is unavailable;
- the target repository state makes safe synchronization impossible;
- a project/Skill authority is missing or contradictory;
- continuing would cross a human, scientific, product, or trust boundary without
  authorization.

## Boundaries

- This Skill routes collaboration; `references/*` owns this repository's current
  operational policy.
- Project-specific truth remains in the owning project.
- A project may declare selected concepts as canonical design authority; its
  Skills/references must conform as operational projections.
- This repository's concepts remain decision history/rationale.
- Do not create a Codex task when ChatGPT can safely and completely do the work with
  its connected tools.
