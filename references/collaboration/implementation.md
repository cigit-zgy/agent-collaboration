# AI-assisted implementation contract

Load this reference for ChatGPT-first code authorship, AI implementation quality, reviewability, engineering discipline, dependencies, documentation, and implementation transparency.

Prior-art design is owned by `../project/prior-art.md`; verification level/placement by `verification.md`; GitHub Actions by `actions.md`; maintained Skill design/testing lifecycle by `../skill/development.md`.

## Operating model

```text
User
= scientific/product/design decision authority
= chooses goals, principles, trust boundaries, important tools, and required human approvals
= is not required to write code or line-review every change

ChatGPT
= design partner + connected author/executor + acceptance reviewer
= authors code/tests when repository context and shared coding-Skill authority are sufficient

Codex
= LOCAL execution agent
= environment-bound implementation, verification, debugging, bounded repair
```

Human accountability means accountability for designated decisions/acceptance boundaries, not mandatory human code authorship.

## ChatGPT-first code authoring

ChatGPT should implement every bounded code/test change it can correctly author from:

```text
accepted project design
+ current repository content
+ project tooling/configuration
+ applicable shared coding Skills
+ connected repository write capability
```

The need for later local execution or expensive verification does not by itself transfer code authorship to Codex.

Preferred flow:

```text
ChatGPT writes implementation + tests
→ ChatGPT runs cheap supported checks
→ Codex runs remaining local/environment-bound verification
→ Codex performs bounded evidence-driven repair when needed
→ ChatGPT acceptance review
```

Codex becomes the primary implementation author only when correctness materially depends on a local feedback loop unavailable to ChatGPT, such as browser/runtime behavior, compiled/native dependencies, machine-local services, credentials, proprietary data, hardware, or another local-only interface.

Do not delegate an entire implementation merely because one verification step is local.

## Design before custom implementation

For a new project/core subsystem/major algorithm/architecture/tool choice, the applicable prior-art and concept gate must already be resolved before substantial custom implementation.

Implementation preference is:

```text
existing project implementation/pattern
→ accepted prior-art REUSE candidate
→ accepted ADAPT component/pattern
→ mature existing library/tool
→ smallest direct implementation for the proven remaining gap
→ new abstraction only when a real current owner/consumer requires it
```

Do not reimplement a capability merely because new code is faster to write than an existing strong implementation is to understand.

If an accepted external candidate no longer fits, return the design consequence to User + ChatGPT rather than silently inventing a replacement architecture.

## Maintained Skill changes

For first-party Skill behavior changes:

```text
concept/design authority
→ SKILL.md + references
→ implementation
→ design-probing tests
```

If the durable Skill contract is ambiguous, do not patch production code around the current task/example. Use `../skill/development.md`.

Pure implementation drift may be repaired directly when the existing concept/Skill Markdown already determines the expected behavior without interpretation.

## Shared coding-Skill authority

ChatGPT-authored and Codex-authored code in one task follows the same applicable coding-Skill revisions/modes.

Detailed immutable coordinates, activation, precedence, and local alignment are owned by `shared-coding-skills.md`.

Project `AGENTS.md`, accepted scientific/product design, and project tooling take precedence over generic coding Skills.

## Equal quality standard

AI-produced code is held to the same maintained-code standard expected from human-authored implementation.

Passing tests alone is insufficient. The implementation must be understandable, maintainable, consistent with the accepted contract, appropriately documented, and supported by evidence proportionate to risk.

## Transparency

For material implementation work, the execution result/report should make these recoverable when applicable:

```text
what ChatGPT authored before local handoff
what Codex added/repaired after local execution
which shared coding Skills/revisions governed the work
key implementation choice + design-relevant rationale
main data/control flow affected
important invariants/failure boundaries
new/removed dependencies or abstractions
known limitations/deviations/non-goals
how the implementation was verified
```

Do not turn production code into a transcript of AI reasoning. Transparency belongs primarily in durable task/report evidence, tests, clear names, and concise comments around non-obvious constraints.

## Reviewability and change size

Prefer bounded logical changes that can be explained and verified as one responsibility.

There is no universal line-count limit. Decompose when a change spans independent responsibilities, unrelated architectural concerns, several trust boundaries, or a diff too large to explain/verify coherently.

```text
one bounded responsibility
→ implement
→ verify
→ acceptance review
→ next responsibility
```

AI generation capacity is not a reason to create a large review burden.

## Engineering discipline

Understand current execution/data flow before adding structure.

Prefer the smallest sufficient implementation that satisfies the accepted contract.

Do not add abstractions, dependencies, manifests, state files, registries, caches, hashes, freshness mechanisms, compatibility layers, wrappers, forwarding layers, or duplicate tests for hypothetical future use or reassurance alone.

A shared abstraction needs a real current owner + consumer. A persistent integrity mechanism needs an identifiable trust/provenance boundary + current consumer.

Scientific correctness, product semantics, security, data-loss prevention, reproducibility, and trust boundaries take precedence over implementation minimalism.

## Existing patterns and mechanical style

Use target-repository patterns when compatible with accepted design.

Mechanical style belongs to project runtime/tooling authority, for example:

```text
pyproject.toml
formatter/linter config
type checker config
test config
pre-commit / CI when present
```

Do not duplicate language-specific style manuals in collaboration prose when tooling can enforce them.

If the project has no mechanical style authority, use maintained ecosystem conventions and keep the implementation internally consistent rather than inventing a framework.

## Verification boundary

Implementation authorship and verification placement are separate decisions.

ChatGPT runs cheap directly available checks; Codex runs setup-heavy/time-consuming/project-environment/real-artifact work. Detailed evidence selection is owned by `verification.md`.

GitHub Actions is a separate hosted-evidence concern owned by `actions.md`. Do not duplicate a Codex-proven claim in Actions unless the hosted environment proves a distinct property.

Code written but missing required execution evidence is `implemented, awaiting verification`; it is not accepted merely by inspection.

## Documentation and comments

Document public behavior and non-obvious scientific, algorithmic, trust, or failure semantics when future maintainers need them.

Avoid comments/docstrings that merely narrate obvious code, repeat types, restate function names, or create prose likely to drift from implementation.

## Dependencies and external tools

Add a dependency only when the current task has a concrete need better served by that dependency than by an existing capability, accepted prior-art candidate, or small direct implementation for a proven gap.

For evolving external CLIs/APIs/schemas, use the project external-tool adapter contract. Do not guess renamed flags, silently substitute tools, or infer semantic compatibility from successful execution alone.

## High-risk implementation

Scientific semantics, public contracts, trust-state transitions, destructive migrations, credentials/secrets, security-sensitive behavior, and release-critical infrastructure require the higher design/verification/human checkpoints declared by project/collaboration authority.

Codex does not resolve genuine scientific/product/design ambiguity by inventing behavior in code.

## Completion

Implementation is complete only when:

```text
accepted semantics are implemented
AND applicable prior-art/Skill-design decisions are respected
AND applicable shared coding Skills are aligned
AND the change is reviewable/maintainable
AND required mechanical checks pass
AND required evidence exists without unjustified duplication
AND material limitations/deviations are disclosed
AND required ChatGPT acceptance/User checkpoint is satisfied
```
