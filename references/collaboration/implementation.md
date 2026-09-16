# AI-assisted implementation contract

Load this reference for implementation quality, authorship, dependencies, engineering discipline, or reviewability.

## Operating model

```text
User    = scientific/product/design authority
ChatGPT = connected author/executor + acceptance reviewer
Codex   = local implementation/execution/verification/repair
```

Inside an already accepted scope, routine reversible implementation choices belong to the Agent. Do not ask the User to choose ordinary code structure, naming, test arrangement, or repair steps unless the choice changes product/scientific meaning or crosses another real decision boundary.

## Author where feedback exists

ChatGPT should author bounded code/tests when repository context and connected capabilities are sufficient.

Codex becomes the primary implementation author when correctness materially depends on local feedback unavailable to ChatGPT: project runtimes, native dependencies, browser behavior, machine-local services, credentials, proprietary data, hardware, or similar environment-bound evidence.

Do not delegate an entire deliverable merely because one verification step is local.

## Design boundary

Implementation follows accepted Design/Skill semantics. If those semantics do not determine the expected behavior, stop the affected semantic path and return the ambiguity upstream rather than encoding a task-local guess.

Pure implementation drift may be repaired directly when current authority already determines the expected behavior.

## Engineering principles

Prefer, in order:

```text
existing project pattern
→ authoritative, maintained third-party dependency/tool
→ smallest direct implementation for the proven gap
→ new abstraction only when a real current consumer needs it
```

Do not reimplement a substantial capability that is already provided by a suitable mature dependency merely to keep all code in-repository.

When choosing among third-party candidates, weigh the signals in this order when relevance is comparable:

```text
official / standards-body / original-author / established ecosystem provenance
→ active maintenance and recent compatible releases
→ fit with the required API/semantics/runtime
→ license, security posture, documentation and tests
→ ecosystem adoption and long-term stability
→ stars, forks, downloads or similar popularity signals
```

Popularity is supporting evidence, not authority. Do not impose a universal minimum star count: niche scientific or standards libraries may be authoritative with modest popularity, while a high-star repository may be stale or unsuitable.

Prefer the mature dependency when it materially reduces custom code and maintenance burden without compromising scientific/product semantics, reproducibility, security, licensing, deployment, or runtime constraints.

Do not add a heavy dependency for a trivial capability when a small direct implementation is clearer and lower-maintenance. New dependencies must serve a concrete current need.

Keep changes reviewable and responsibility-bounded. Do not add registries, caches, wrappers, compatibility layers, state files, hashes, dependencies, or helper frameworks for hypothetical future use.

Scientific correctness, product semantics, reproducibility, security, and data-loss prevention outrank code minimalism.

## Follow-through

For in-scope failures caused by the change:

```text
inspect → diagnose → repair → rerun
```

Continue until the requested outcome and completion criteria are met or a true blocker/decision boundary is reached.

## Style and tooling

Use target-repository patterns and mechanical tooling when present. Shared coding Skills are secondary guidance and do not override project Design or explicit User instructions.

Comments/docstrings should explain non-obvious public, scientific, algorithmic, trust, or failure semantics—not narrate obvious code.

## Dependencies

Before adding meaningful custom functionality that is likely to exist in a mature library or tool, inspect established third-party options first. For substantial framework/tool choices, use the project prior-art gate.

Add a dependency only for a concrete current need that it satisfies better than an existing capability or a small direct implementation.

Record or pin the dependency/version/profile to the degree required by the project's reproducibility and compatibility contract; do not cargo-cult exact pins when the project intentionally supports a validated compatible range.

For independently evolving external interfaces, use the project adapter boundary and explicit compatibility evidence; do not infer semantic compatibility from a successful command alone.

## Verification

Verification effort is selected by `verification.md`. Passing tests alone is not enough if the task claims a broader scientific/product/integration property, but do not broaden testing beyond the actual claim without a reason.

## Completion

Implementation is complete when the accepted semantics are implemented, the change is maintainable and reviewable, required checks establish the intended claim, material limitations are disclosed, and no required User checkpoint remains.
