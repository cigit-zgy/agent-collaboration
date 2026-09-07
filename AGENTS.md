# agent-collaboration repository context

## Identity

This repository is the maintained first-party source for the `agent-collaboration` Skill: the reusable User ↔ ChatGPT ↔ Codex operating contract used across maintained projects and Skills.

## Authority

```text
AGENTS.md
= repository-maintenance constitution

SKILL.md
= sole runtime routing index

references/
= current operational owners

reports/concept/
= collaboration decision history/rationale

reports/chatgpt/
= durable ChatGPT-authored Codex task specifications

reports/codex/
= FORMAL Codex execution evidence only
```

User + ChatGPT maintain collaboration design. The User retains final decision/override authority and designated human checkpoints. ChatGPT performs connected DIRECT authoring and acceptance review. Codex executes approved LOCAL work and does not self-accept.

## Owner map

### Collaboration

```text
references/collaboration/protocol.md
= roles, authority, refresh, instruction/data trust, semantic ownership

references/collaboration/execution.md
= DIRECT/LOCAL-QUICK/FORMAL route selection, durable Codex-task handoff, remote synchronization, Git/worktree/tmp/concurrency

references/collaboration/formal.md
= FORMAL task/report lifecycle, acceptance, report lookup, integration

references/collaboration/implementation.md
= ChatGPT-first/AI-assisted implementation quality and engineering discipline

references/collaboration/verification.md
= verification levels, evidence categories, ChatGPT/Codex placement

references/collaboration/actions.md
= GitHub Actions hosted-claim, public/private, trigger/budget policy

references/collaboration/shared-coding-skills.md
= cross-Agent coding-Skill authorities/alignment

references/collaboration/agents.md
= AGENTS.md writing standard

references/collaboration/templates/
= cold LOCAL-QUICK/FORMAL task/report formats
```

### Project

```text
references/project/architecture.md
= project ownership/integration responsibility map

references/project/migration.md
= existing-project migration to current collaboration architecture with low-context bootstrap

references/project/reports.md
= report families, task/report semantics, filenames/metadata, archive placement

references/project/concept.md
= chronological concept-journal semantics; design history/input only

references/project/design.md
= canonical current living-design tree + dynamic topic decomposition

references/project/prior-art.md
= external prior-art/reuse gate before substantial new design

references/project/external-tools.md
= external CLI/API/schema adapter/profile/reproducibility

references/project/handoff.md
= conversation migration/recovery contract

references/project/templates/
= cold project authoring/bootstrap templates
```

### Skill

```text
references/skill/development.md
= current design → Skill Markdown → implementation → design-probing tests

references/skill/writing.md
= SKILL.md/reference writing and progressive-disclosure standard

references/skill/repository.md
= maintained source/discovery/distribution

references/skill/package.md
= Skill package/resources/runtime ownership
```

Each current concern has one operational owner.

## Maintenance routing

Read `SKILL.md` first for runtime intent routing. For repository maintenance, select only the directly owning reference.

```text
change roles/authority/trust           → protocol.md
change Codex delegation/Git/tmp/sync   → execution.md
change FORMAL task/acceptance          → formal.md + exact template if needed
change Actions policy                  → actions.md
change verification model              → verification.md
change existing-project migration      → project/migration.md
change report/task/archive contract    → project/reports.md
change concept-journal semantics       → project/concept.md
change current living-design semantics → project/design.md
change project integration             → project/architecture.md
change external tool policy            → project/external-tools.md
change Skill behavior lifecycle        → skill/development.md
change Skill Markdown standard         → skill/writing.md
```

Do not preload all owners or historical reports.

## Runtime and verification

This repository owns no independent executable runtime by default. Documentation-only policy changes use direct structural/link/ownership review.

ChatGPT authors code/tests it can correctly produce from repository context/shared Skill authority. Local or time-consuming evidence belongs to Codex. GitHub-hosted CI exists only for distinct hosted claims under `actions.md`.

## Hard invariants

- `SKILL.md` is the sole runtime routing index; do not add a mandatory second reference index.
- Every repository task delegated to Codex, including LOCAL-QUICK, MUST be committed/pushed first under `reports/chatgpt/YYMMDD_chatgpt_NN.md`.
- The committed ChatGPT task is the sole task-specific execution specification; detailed task bodies MUST NOT be pasted into chat.
- User-visible Codex handoff is locator-only: at most one short sentence plus one fenced `text` block with task coordinates and immutable link.
- Every repository-changing Codex task MUST fresh-fetch before mutation, prove local execution HEAD equals the authorized fetched remote baseline, then after commit/push fresh-fetch again and prove local task HEAD equals fetched upstream HEAD. Without final equality, PASS is forbidden.
- Remote synchronization does not authorize blind `git pull`, reset, rebase, stash, force checkout, or force push; preserve pre-existing User state and use a safe task branch/worktree.
- LOCAL-QUICK creates no `reports/codex/` report; FORMAL does.
- If a task artifact cannot be pushed, do not substitute a long chat-only task.
- Templates and historical reports are cold paths unless the active task creates/reviews that artifact.
- Existing-project migration uses repository-native current state plus a compact bootstrap; do not require old-conversation reconstruction.
- `reports/concept/` is design history/input; current project design authority lives in one `design/` tree when that model is used.
- A project `design/` tree contains current accepted semantics only; no old/draft/versioned parallel designs.
- Project-specific scientific facts remain in the owning source/evidence chain.
- ChatGPT and Codex use the same immutable authority for every material shared coding Skill.
- Skill behavior changes follow current design → Skill Markdown → code → design-probing tests.
- Local verification need alone does not transfer all code authorship from ChatGPT to Codex.
- Conversation handoffs are context only; they never override current authority/state.
