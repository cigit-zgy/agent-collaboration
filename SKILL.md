---
name: agent-collaboration
description: >
  Coordinate User, ChatGPT, and Codex for repository work that needs design,
  direct remote action, committed local execution, verification, independent audit,
  project onboarding, or Skill onboarding.
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
- Standalone first-party Skill repository onboarding:
  `references/skill-repository-policy.md` → `references/skill-agents-template.md` →
  `references/skill-package-architecture.md` → the appropriate template under
  `references/skill-templates/`.
- Formal Codex task authoring: `references/chatgpt-task-template.md` plus the
  selected level from `references/verification-levels.md`.
- Codex launch: `references/codex-launch-template.md`.
- Codex execution report: `references/codex-report-template.md`.
- Report/concept lifecycle: `references/report-concept-policy.md`.
- Verification-tool selection: `references/verification-tools.md`.
- Skill/project environment ownership: `references/skill-environment-policy.md`.

## Progressive disclosure

Load only the active route:

```text
applicable AGENTS.md
→ this SKILL.md
→ one owning reference
→ target project workflow SKILL.md when relevant
→ owning sub-Skill
→ only resources required by that Skill
```

Do not read project concepts by default. Read `reports/concept/README.md` and a
specific concept only when historical design rationale or supersession is needed.

## Skill discovery boundary

Maintained source under `/Users/wenv/Documents/skills/` is not itself the canonical
Codex discovery location. Current Codex local discovery uses `.agents/skills`
locations; reusable external distribution should use the platform's supported plugin
or another explicit distribution artifact. The authoritative local policy is
`references/skill-repository-policy.md`.

## Stop conditions

Stop and surface the issue instead of improvising when:

- a design-affecting decision remains unresolved;
- the required local capability is unavailable;
- the target repository state makes safe synchronization impossible;
- a project/Skill authority is missing or contradictory;
- continuing would cross a human, scientific, product, or trust boundary without
  authorization.

## Boundaries

- This Skill routes collaboration; `references/*` owns current operational policy.
- Project-specific truth remains in the owning project.
- Concepts record decision history/rationale and do not override operational
  references.
- Do not create a Codex task when ChatGPT can safely and completely do the work with
  its connected tools.
