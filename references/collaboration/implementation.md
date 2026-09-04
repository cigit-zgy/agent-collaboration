# AI-assisted implementation contract

This contract governs code and executable implementation produced through ChatGPT/Codex collaboration.

## Operating model

The collaboration may use a zero-human-coding model:

```text
User
= scientific/product/design decision authority
= chooses goals, principles, trust boundaries, important tools, and required human approvals
= is not required to write code or perform line-by-line code review

ChatGPT
= design partner and acceptance reviewer
= completes connected DIRECT design and implementation work
= authors code/tests when repository context and shared coding-Skill authority are sufficient

Codex
= LOCAL execution agent
= performs environment-bound implementation, verification, debugging, and bounded repair

project tooling / CI
= mechanical enforcement and reproducible evidence
```

Human accountability therefore means accountability for designated human decisions and acceptance boundaries, not an obligation for the User to author or manually inspect every line of implementation.

## ChatGPT-first code authoring

ChatGPT should implement every bounded code/test change it can correctly author from:

```text
accepted project design
+ current repository content
+ project tooling/configuration
+ applicable shared coding Skills
+ available connected repository write capability
```

The need for later local execution or expensive verification does **not** by itself transfer code authorship to Codex.

Preferred flow:

```text
ChatGPT writes implementation + tests
→ ChatGPT runs only cheap supported checks
→ commit/push task branch
→ Codex runs remaining local/environment-bound verification
→ Codex performs bounded implementation repair when evidence requires it
→ ChatGPT acceptance review
```

Codex becomes the primary implementation author only when correct implementation materially depends on an iterative local feedback loop that ChatGPT cannot access, such as browser/runtime behavior, compiled/native dependencies, machine-local services, credentials, proprietary data, hardware, or another local-only interface.

Do not delegate an entire implementation merely because one verification step is local.

## Shared coding-Skill authority

ChatGPT-authored and Codex-authored code in one task must follow the same applicable coding-Skill revisions and modes.

Use:

```text
shared-coding-skills.md
```

for immutable Skill coordinates, precedence, task activation, local alignment, and update policy.

A machine-local discovery path or Skill name alone is not enough. ChatGPT must be able to resolve the actual Skill content it claims to follow. Codex's locally discovered copy must not silently override the task-pinned shared authority.

Project `AGENTS.md`, accepted scientific/product design, and project tooling remain higher authority than generic coding Skills.

## Equal quality standard

AI-produced code must meet the same quality standard expected from maintained human-produced code.

A change is not acceptable merely because it was generated quickly or because tests happen to pass. The implementation must be understandable, maintainable, appropriately documented, consistent with the accepted contract, and supported by evidence proportionate to its risk.

## Transparency

AI-assisted implementation must leave enough information for another maintainer or Agent to understand what was changed and why without reconstructing the generation conversation.

For a material implementation change, the execution result or formal Codex report should make the following recoverable when applicable:

```text
what ChatGPT authored before local handoff
what Codex added or repaired after local execution
which shared coding Skills and revisions governed the work
why the implementation was chosen
main data/control flow affected
important invariants or failure boundaries
new or removed dependencies/abstractions
known limitations or deliberate non-goals
how the implementation was verified
```

Do not turn production code into a transcript of AI reasoning. Transparency belongs primarily in task/report evidence, tests, clear names, and concise comments around non-obvious constraints.

## Reviewability and change size

Prefer bounded logical changes that can be explained and verified as one responsibility.

There is no universal line-count limit. Decompose a change when it spans independent responsibilities, unrelated architectural concerns, several trust boundaries, or a diff too large to explain and verify coherently in one acceptance review.

The governing pattern is:

```text
one bounded responsibility
→ implement
→ verify
→ acceptance review
→ next responsibility
```

Do not use AI's ability to generate large amounts of code as a reason to create a large review burden.

## Engineering discipline

Understand the current execution and data flow before adding structure.

Prefer the smallest sufficient implementation that satisfies the accepted contract.

Prefer, in order:

```text
existing project implementation/pattern
→ mature existing library/tool
→ direct local implementation
→ new abstraction only when a real current responsibility and consumer require it
```

Do not add abstractions, dependencies, manifests, state files, registries, caches, hashes, freshness mechanisms, compatibility layers, wrappers, forwarding layers, or duplicate tests for hypothetical future use or reassurance alone.

A shared abstraction needs a real current owner and real current consumers. A persistent integrity mechanism needs an identifiable trust/provenance boundary and a current consumer.

Scientific correctness, product semantics, security, data-loss prevention, reproducibility, and trust boundaries take precedence over implementation minimalism.

## Existing patterns and mechanical style

Use the target repository's existing patterns when they remain compatible with the accepted design.

Mechanical code style belongs to the project runtime/tooling authority, for example:

```text
pyproject.toml
Ruff / formatter configuration
type checker configuration
test configuration
pre-commit / CI when present
```

Do not duplicate a language-specific style manual in this collaboration contract when tooling can enforce the rule directly.

If the project has no mechanical style authority, use the language ecosystem's conventional maintained style and keep the implementation internally consistent rather than inventing a project-specific framework.

## Verification placement for speed

Implementation authorship and verification location are separate decisions.

ChatGPT performs checks that are cheap and directly available without substantial environment setup, for example structural/diff inspection, syntax checks, small pure tests in an available online runtime, or reading existing remote CI results.

Codex performs checks whose cost or evidentiary value depends on the User's local environment, including project environments, full suites, builds, browsers, external CLIs/services, proprietary data, hardware, large artifacts, or long-running E2E/recovery work.

Do not duplicate an expensive check remotely and locally unless the second environment provides a distinct required claim. The detailed placement rules are in `verification.md`.

Code that ChatGPT has written but that has not yet received required execution evidence must be described as implemented but awaiting local verification; it is not accepted merely by inspection.

## Documentation and comments

Document public behavior and non-obvious scientific, algorithmic, trust, or failure semantics when future maintainers need that information.

Avoid comments or docstrings that merely narrate obvious code, repeat types, restate function names, or create long prose that can drift from implementation.

## Dependencies and external tools

Add a dependency only when the current task has a concrete need that is better served by that dependency than by an existing project capability or a small direct implementation.

For evolving external CLIs/APIs/schemas, follow the owning project's adapter boundary. Do not guess renamed flags, silently substitute tools, or infer semantic compatibility from successful execution alone.

## High-risk implementation

Changes involving scientific semantics, public contracts, trust-state transitions, destructive migrations, credentials/secrets, security-sensitive behavior, or release-critical infrastructure require the higher design/verification/human checkpoints defined by the project and collaboration protocol.

Codex does not resolve a genuine scientific/product/design ambiguity by inventing behavior in code.

## Completion criterion

Implementation work is complete only when:

```text
accepted semantics are implemented
AND the applicable shared coding Skills were resolved consistently
AND the change is reviewable and maintainable
AND required mechanical checks pass
AND required risk-based evidence is available
AND material limitations/deviations are disclosed
AND ChatGPT acceptance review is completed when the collaboration route requires it
```
