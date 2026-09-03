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
= completes connected DIRECT work
= specifies and reviews delegated implementation

Codex
= implementation executor for LOCAL work
= may write, modify, test, debug, and refactor the code in scope

project tooling / CI
= mechanical enforcement and reproducible evidence
```

Human accountability therefore means accountability for designated human decisions and acceptance boundaries, not an obligation for the User to author or manually inspect every line of implementation.

## Equal quality standard

AI-produced code must meet the same quality standard expected from maintained human-produced code.

A change is not acceptable merely because it was generated quickly or because tests happen to pass. The implementation must be understandable, maintainable, appropriately documented, consistent with the accepted contract, and supported by evidence proportionate to its risk.

## Transparency

AI-assisted implementation must leave enough information for another maintainer or Agent to understand what was changed and why without reconstructing the generation conversation.

For a material implementation change, the execution result or formal Codex report should make the following recoverable when applicable:

```text
what changed
why this implementation was chosen
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
AND the change is reviewable and maintainable
AND required mechanical checks pass
AND required risk-based evidence is available
AND material limitations/deviations are disclosed
AND ChatGPT acceptance review is completed when the collaboration route requires it
```
