---
id: 10_github_actions_budget_and_verification_placement
title: GitHub Actions budget and verification placement
status: active
role: decision_history
operational_authority:
  - references/collaboration/verification.md
  - references/collaboration/implementation.md
---

# GitHub Actions budget and verification placement

## Decision

GitHub Actions is not a default second test layer. It is used only when GitHub-hosted execution proves a distinct claim that ChatGPT/Codex/local project tooling does not already establish.

The accepted verification model is:

```text
ChatGPT
→ authoring + cheap connected checks

Codex local
→ project/runtime/browser/data/build/E2E verification

GitHub Actions
→ independent clean-room / runtime matrix / GitHub status gate / release-publish / public-reproducibility evidence only
```

A command being runnable in Actions does not justify running it there. If Codex has already established the same verification claim in an appropriate environment, repeating the same Ruff/pytest/type/build/render claim in Actions adds no required evidence and should be removed, narrowed, or made manual.

## Repository visibility policy

Private repositories default to no automatic `push`/`pull_request` Actions. Ordinary verification is performed by ChatGPT + Codex locally. A private workflow is justified only by a concrete hosted-environment claim worth the account's current Actions budget; milestone/release checks should normally use narrow manual/tag/release triggers and the smallest sufficient matrix.

Public repositories may retain standard GitHub-hosted CI when it materially improves public reproducibility, contributor feedback, GitHub status checks, packaging, or release confidence. Public status does not waive claim deduplication: free redundant CI remains redundant engineering work.

GitHub billing and runner-pricing details are external platform facts rather than frozen collaboration semantics. Recheck current official GitHub documentation whenever billing materially affects a repository decision; larger/special runners, storage, artifacts, caches, and similar resources are treated separately from standard-runner minutes.

## Why

The User's account reached 90% of its included Actions minutes while many ordinary checks were already reproducible through local Codex execution. The collaboration therefore separates verification capability from verification placement and reserves GitHub-hosted execution for evidence that is actually distinct.

This preserves Actions value for important scientific/release work while avoiding repeated expenditure on ordinary private-repository development.

## Operational projection

Current rules live in:

- `references/collaboration/verification.md` — Actions claim deduplication, private/public defaults, trigger/matrix guidance, and budget review;
- `references/collaboration/implementation.md` — Codex/Actions duplication prohibition during implementation.

Future project-level workflow changes should conform to those owners rather than copying this history file.
