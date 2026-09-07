# Token-efficient progressive-disclosure architecture

## Status

Accepted collaboration design history. Current operational authority is projected into `SKILL.md` and `references/`.

## Problem

`agent-collaboration` has grown into a multi-concern Skill used by many repositories. The main risk is no longer missing policy; it is context overhead and routing ambiguity. A normal task must not load collaboration-wide policy, templates, history, and unrelated project/Skill guidance merely to find one owning rule.

The design objective is:

```text
one Skill trigger
→ one thin runtime router
→ one primary owning reference
→ at most one explicitly named secondary owner when the task truly spans concerns
```

Historical reports, templates, examples, and unrelated owners remain cold paths.

## Prior-art basis

### OpenAI Skills

OpenAI's maintained Skill creator uses a three-level loading model: metadata is always available, `SKILL.md` loads when the Skill triggers, and bundled `references/`/scripts/assets are loaded or used only as needed. It also treats the frontmatter description as the main trigger surface and advises against extraneous documentation that adds context clutter.

Design consequence: `SKILL.md` must remain the runtime entry/router; supporting material belongs in on-demand resources rather than another mandatory runtime index.

Source: `openai/skills`, `skills/.system/skill-creator/SKILL.md`.

### Anthropic Agent Skills

Anthropic's Skill creator uses the same progressive-disclosure model and recommends keeping the core Skill compact, moving specialized material to references, and adding navigation/TOC support for large reference material.

Design consequence: large multi-trigger owners should split by independent concern, while coherent owners should not be fragmented merely to reduce file size.

Source: `anthropics/skills`, `skills/skill-creator/SKILL.md`.

### Trail of Bits Skills

Trail of Bits explicitly recommends progressive disclosure and a one-level-deep reference model: `SKILL.md` links directly to the needed files; reference chains should not become `SKILL.md → file1 → file2` dependency ladders.

Design consequence: do not add a mandatory `references/INDEX.md` between `SKILL.md` and the owning reference. Direct read sets live in `SKILL.md`.

Source: `trailofbits/skills`, `AGENTS.md` / `CLAUDE.md`.

### GitHub Copilot agent guidance

GitHub's `awesome-copilot` guidance for orchestrated agents recommends passing only essential context and having specialized agents read their own governing specification.

Design consequence: collaboration routing should identify the smallest responsible owner instead of forwarding a broad context bundle.

Source: `github/awesome-copilot`, agent/instruction guidance.

## Accepted architecture

### 1. `SKILL.md` is the sole runtime index

Do not introduce a second mandatory runtime index under `references/`.

`SKILL.md` owns:

```text
Skill purpose / trigger
minimal operating model
intent → direct owner read set
cold-path loading rules
completion routing
```

It does not restate the detailed contents of each owner.

### 2. Direct read sets

Every common intent is routed directly from `SKILL.md` to:

```text
one primary owner
+ zero or one secondary owner only when the task genuinely spans concerns
```

A reference should be substantially self-contained for its concern. Do not require a normal reader to follow a reference chain to understand the owner it was routed to.

### 3. Hot / warm / cold paths

```text
HOT
- SKILL.md frontmatter + thin router

WARM
- one primary owning reference
- optional second owner explicitly selected by the router

COLD
- templates unless creating that artifact
- reports/concept history
- reports/chatgpt and reports/codex except the active task/report
- old handoffs
- examples/assets unrelated to the active task
```

Ordinary execution MUST NOT preload cold paths.

### 4. Concern splits

Split only when a file has multiple independent activation conditions and normal readers frequently need only one part.

Accepted splits:

```text
collaboration/protocol.md
→ core roles / authority / trust / semantic ownership only

collaboration/execution.md
→ DIRECT / LOCAL-QUICK / FORMAL route selection, Git safety, tmp/worktree/concurrency

collaboration/formal.md
→ committed task/report lifecycle, handoff, acceptance, report lookup, integration

collaboration/verification.md
→ verification levels, evidence categories, ChatGPT/Codex placement

collaboration/actions.md
→ GitHub Actions distinct-claim, public/private, trigger/budget policy

project/architecture.md
→ project ownership / integration / runtime route

project/external-tools.md
→ external CLI/API/schema adapter, known-profile and reproducibility boundary

project/handoff.md
→ handoff authority/trigger/index/recovery/lifecycle

project/templates/handoff.md
→ handoff metadata/body/authoring template
```

### 5. Cohesive owners remain intact

Do not split these merely for size while their concern remains coherent:

```text
collaboration/implementation.md
collaboration/shared-coding-skills.md
project/concept.md
project/prior-art.md
skill/development.md
skill/writing.md
skill/repository.md
skill/package.md
```

Cross-owner duplication should be reduced instead.

## Context-budget targets

These are design signals, not parser-enforced byte quotas.

```text
SKILL.md runtime router
→ target roughly <= 250 lines; never grow into a policy manual

owning reference
→ target roughly <= 300 lines when practical
→ if materially longer, add a TOC or split only when multiple activation conditions exist

normal collaboration read set
→ one primary owner
→ optional second owner only when necessary
→ zero historical report preload

reference depth
→ SKILL.md → owner
→ no mandatory owner → owner chain
```

For ordinary implementation, verification, Skill maintenance, GitHub Actions review, or context recovery, the expected collaboration context should be a small fraction of the complete repository.

## Routing-quality criteria

Representative routing evaluation should test intents such as:

```text
ordinary implementation
verification planning
GitHub Actions review
LOCAL execution / worktree cleanup
FORMAL task creation
FORMAL completion / acceptance
Skill design
Skill implementation drift
Skill testing
new project / prior-art design
external tool integration
conversation migration/recovery
shared coding-Skill alignment
```

The design is healthy when:

```text
correct owner selected
normal route depth <= 1 reference hop from SKILL.md
unrelated owner preload = 0
history preload = 0
no task requires browsing the whole repository merely to discover its owner
```

If an Agent must read several large collaboration files before it can determine the correct owner, classify that as a routing/design gap rather than normal operating cost.

## Operational projection

This decision projects to:

```text
SKILL.md
AGENTS.md
README.md
references/collaboration/protocol.md
references/collaboration/execution.md
references/collaboration/formal.md
references/collaboration/verification.md
references/collaboration/actions.md
references/project/architecture.md
references/project/external-tools.md
references/project/handoff.md
references/project/templates/handoff.md
references/skill/writing.md
project / Skill AGENTS templates
reports/concept/README.md
```
