# AI-assisted implementation and governance simplification — decision history

## Context

The collaboration is intended to support a zero-human-coding workflow for maintained scientific/software projects.

The User's role is to make necessary scientific, product, design, trust, and tool-selection decisions. ChatGPT and Codex may produce all implementation code. Reliability therefore depends on explicit authority, transparent AI implementation, bounded changes, machine-verifiable evidence, and acceptance review rather than on requiring the User to write or line-review code.

A review of the previous collaboration protocol also identified governance overhead that could itself create failures, especially shared-default-branch freezes, mandatory formal tasks for trivial repository edits, whole-file frozen DIRECT rules, and a mandatory six-row verification-layer matrix.

External evidence considered during the redesign included AI-assisted contribution practices such as LlamaIndex's emphasis on transparency, human accountability, equal quality standards, small/reviewable changes, and avoiding unreviewed architectural rewrites. An adversarial review of the collaboration repository was treated as evidence rather than authority and was selectively accepted or rejected.

## Accepted decisions

### Zero-human-coding accountability

Human accountability is decision accountability, not mandatory human code authorship.

```text
User
→ scientific/product/design/tool decisions + final override

ChatGPT
→ design/direct work + acceptance review

Codex
→ LOCAL implementation/execution

project tooling/CI
→ mechanical enforcement/evidence
```

### AI implementation transparency

AI-produced implementation must meet the same maintained-code quality standard as human-produced implementation and leave an auditable explanation of material implementation choices, affected flow/invariants, dependencies/abstractions, limitations, and verification.

This information belongs primarily in execution/report evidence, tests, clear code structure, and concise non-obvious comments rather than in verbose generated commentary inside production code.

### Reviewability

AI generation capacity is not permission for oversized diffs. Independent responsibilities should be implemented and accepted incrementally. No universal LOC threshold is imposed.

### Engineering discipline as repository-recoverable authority

The collaboration repository now owns a dedicated AI-assisted implementation contract. It captures smallest-sufficient implementation, reuse of existing patterns/mature tools, resistance to speculative abstractions/dependencies/compatibility layers, and the separation between engineering principles and project-specific mechanical style/tooling.

### LOCAL-QUICK

Small, low-risk repository changes no longer require the full formal task/report path merely because repository state changes. LOCAL-QUICK provides a bounded Codex implementation route with focused verification, commit/push when applicable, and ChatGPT acceptance review.

FORMAL remains appropriate for major architecture, scientific/trust/public-contract changes, persistent/destructive shared state, long tasks, high-risk work, and release qualification.

### Task branch as FORMAL default

Repository-changing FORMAL work defaults to a dedicated task branch/worktree. The shared default branch is not globally frozen merely because an isolated formal task is running.

Independent default-branch progress is reconciled once at integration rather than automatically blocking an otherwise valid task.

### Semantic freeze instead of whole-file freeze

The real protected object is accepted scientific/product/design semantics and named contracts/invariants. Entire files are not read-only by default. Narrow mechanical projection edits may be permitted explicitly when they cannot alter design meaning.

### Acceptance terminology

ChatGPT review after Codex execution is called `acceptance review`, not automatically `independent review`, because ChatGPT may also have designed or specified the work.

A genuinely independent second model/reviewer/human perspective is added selectively for material LEVEL 2/3 scientific, architecture, trust, security, or release risk.

### Verification categories

LEVEL 1 / LEVEL 2 / LEVEL 3 remain the rigor/cost model.

The six previous "layers" are retained as useful evidence categories rather than being claimed as a strictly orthogonal scale hierarchy. Formal tasks list only categories that are actually required; irrelevant `N/A` rows are removed.

### Instruction/data trust boundary

Ordinary repository and scientific source content is data/evidence, not instruction authority merely because it contains imperative text. Recognized User/AGENTS/Skill/design/formal-task authority controls Agent behavior.

### Component vs integration acceptance

A stage/component may pass while out-of-scope downstream drift remains. That scoped PASS must not be represented as proof that the supported default branch or full pipeline is healthy/release-ready.

## Decisions deliberately not adopted

The redesign did not:

- remove structured verification evidence in favor of pytest-only acceptance;
- impose a fixed LOC threshold for AI changes;
- require an independent second reviewer for every task;
- require PR approval for every repository mutation;
- create a governance linter or task-state database;
- make branch protection or a particular CI provider a universal collaboration requirement;
- allow Codex to redesign accepted scientific/product semantics merely because implementation is difficult.

## Operational projection

Current operational owners are:

```text
references/collaboration/protocol.md
references/collaboration/implementation.md
references/collaboration/verification.md
references/collaboration/templates/chatgpt-task.md
references/collaboration/templates/codex-report.md
```

Project and Skill templates route to those owners rather than duplicating the policy.
