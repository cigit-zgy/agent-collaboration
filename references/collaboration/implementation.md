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
→ accepted reusable dependency/tool
→ smallest direct implementation for the proven gap
→ new abstraction only when a real current consumer needs it
```

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

Add a dependency only for a concrete current need that it satisfies better than an existing capability or small direct implementation.

For independently evolving external interfaces, use the project adapter boundary and explicit compatibility evidence; do not infer semantic compatibility from a successful command alone.

## Verification

Verification effort is selected by `verification.md`. Passing tests alone is not enough if the task claims a broader scientific/product/integration property, but do not broaden testing beyond the actual claim without a reason.

## Completion

Implementation is complete when the accepted semantics are implemented, the change is maintainable and reviewable, required checks establish the intended claim, material limitations are disclosed, and no required User checkpoint remains.
