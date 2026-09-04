---
id: 07
title: Shared coding-Skill alignment and verification placement decisions
status: active
created: 2026-09-03
updated: 2026-09-03
role: decision_history
operational_authority:
  - references/collaboration/implementation.md
  - references/collaboration/shared-coding-skills.md
  - references/collaboration/verification.md
  - references/collaboration/templates/chatgpt-task.md
  - references/collaboration/templates/codex-report.md
  - references/skill/repository.md
related_tasks: []
---

# Shared coding-Skill alignment and verification placement — decision history

## Context

The User's local Codex uses third-party Skills that can materially affect coding style, architecture, testing, and tool choices. ChatGPT may author code through connected GitHub access, but it cannot treat a machine-local discovery path or `LOCAL_SKILLS.md` entry as evidence of the actual Skill content or revision.

Without an explicit shared authority, ChatGPT and Codex can unknowingly implement the same task under different Skill rules.

A second inefficiency was identified: code authorship was too easily delegated in full whenever final verification required the User's local environment, even when ChatGPT could already write the implementation and tests.

## Accepted decisions

### Shared immutable coding-Skill authority

Every third-party coding Skill that materially constrains both ChatGPT and Codex is identified by the same immutable source coordinate:

```text
repository + commit + Skill path + mode/profile
```

Local discovery remains a cache/convenience. It is not cross-Agent authority.

### Small remote profile, complete local inventory

The collaboration/project stores only the small normative cross-Agent coding profile. The machine-local `LOCAL_SKILLS.md` remains the complete local inventory. Third-party Skill bodies are not copied into project or collaboration repositories.

### Task-pinned alignment

Formal tasks pin the collaboration revision and shared coding profile, and identify activated Skills. Codex checks only those Skills before local work.

A mismatch is resolved against the task-pinned revision, not by automatically upgrading both Agents to upstream latest.

### Update review differs from task alignment

```text
task alignment
= use the revision already selected for this task

upstream refresh
= separately review whether a newer revision should become the next profile
```

These operations are not combined implicitly.

### ChatGPT-first code authoring

ChatGPT authors code/tests whenever accepted design, repository content, shared coding Skills, and connected write capability are sufficient. A later need for local verification does not transfer the complete implementation deliverable to Codex.

Codex remains the primary author when correct implementation materially requires an iterative local feedback loop unavailable to ChatGPT.

### Cost-aware verification placement

Cheap checks already supported by ChatGPT's connected/online environment run before handoff. Time-consuming, setup-heavy, project-environment, external-tool, proprietary-data, hardware, browser, and full E2E verification runs through Codex locally.

The same expensive check is not duplicated across environments unless each run proves a distinct claim.

## Operational projection

Current owners are:

```text
references/collaboration/shared-coding-skills.md
references/collaboration/implementation.md
references/collaboration/verification.md
references/collaboration/templates/chatgpt-task.md
references/collaboration/templates/codex-report.md
references/skill/repository.md
```
