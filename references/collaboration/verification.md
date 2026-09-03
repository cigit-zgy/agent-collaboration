# Verification contract

Verification has two dimensions:

```text
verification level
= how much rigor/cost the current task warrants

evidence category
= what kind of evidence is needed to support the specific claim
```

The categories are not a second level system and are not claimed to be mathematically orthogonal system scales. A task selects one verification level and names only the evidence categories materially required by its risks and acceptance claim.

## Verification levels

### LEVEL 1 — FOCUSED

Default for ordinary development and LOCAL-QUICK work.

Typical evidence:

```text
directly affected tests/checks
relevant lint/type checks for touched code
smallest useful smoke/integration check
ChatGPT acceptance review
```

Optimize for fast, relevant feedback.

### LEVEL 2 — MAJOR

Use when a task changes core architecture, scientific/product behavior, an important public contract, a trust boundary, or material cross-module behavior.

Add only evidence justified by those risks, such as contract/integration checks, real-artifact validation, recovery behavior, targeted static/security analysis, or an additional adversarial review perspective.

### LEVEL 3 — RELEASE

Use for release qualification, open-source/release readiness, or security-sensitive release gates.

Add the reproducibility, packaging, clean-install, environment, dependency, static/security, real-artifact, recovery, repeatability, and other non-functional evidence required by the actual release claim.

LEVEL 3 does not mean every available test or scanner must run.

## Evidence categories

### 1. Component / property

Checks small deterministic behavior and local invariants close to the implementation unit.

Examples:

```text
focused pytest
pure-function checks
boundary-value cases
parameterized cases
property-based/fuzz testing when input-space risk warrants it
```

### 2. Contract / invariant

Checks stable public/project-facing behavior independently of implementation details.

Typical targets:

```text
schema and exact fields
file/directory ownership
state transitions
trust-boundary invariants
stable CLI/API behavior
fail-closed conditions
serialization/provenance rules
```

Avoid self-proof where possible: critical expected invariants should not be derived solely from the same production constants or code path being tested.

### 3. Integration

Checks interactions among multiple components inside the in-scope module/stage or across explicitly in-scope adjacent boundaries.

Examples:

```text
component A → component B
CLI → implementation
registry → consumer
adapter → orchestrator
synthetic stage-to-stage handoff
```

Prefer small deterministic fixtures when they adequately represent the interface.

### 4. Real artifact / external tool

Checks behavior that mocks or synthetic inputs cannot establish reliably.

Examples:

```text
real scientific PDFs/data/model files
real parser/simulator/tool execution
real package/resource layouts
representative domain-specific edge cases
```

Reuse stable real artifacts when fresh reconstruction is unnecessary. Rerun expensive external work only when the changed behavior or acceptance claim needs it.

### 5. End-to-end / recovery / repeatability

Checks the complete in-scope flow and adverse state transitions when they materially matter.

Examples:

```text
fresh source → final in-scope artifact
failure → no partial authoritative state
retry/recovery
idempotent reuse
independent reconstructions
cross-run integrity/repeatability
```

Keep E2E evidence sparse; lower-level properties belong at lower-cost categories when that is sufficient.

### 6. Release / non-functional risk

Checks whether a release claim survives outside the developer's current happy-path worktree.

Select only relevant risks, for example:

```text
wheel/sdist or equivalent build
non-editable clean installation
package self-containment
supported OS/Python/runtime matrix
dependency vulnerability audit
static/security analysis
performance/scale/resource limits when claimed
repository/open-source readiness
required CI/status gates when part of repository governance
```

Do not invent irrelevant load, security, or environment tests merely to fill a category.

## Level-to-evidence guidance

Use risk, not ceremony.

```text
LEVEL 1
→ normally Component/property
→ add Contract/Integration when the touched behavior exposes them
→ higher-cost categories only when directly implicated

LEVEL 2
→ cover affected Component/Contract/Integration concerns
→ add Real artifact/external tool when domain/tool reality matters
→ add E2E/recovery/repeatability for trust/transaction/full-flow risk
→ add Release/non-functional only for concrete risk

LEVEL 3
→ cover every evidence category materially required by the release claim
→ commonly includes Contract, Real artifact, E2E/recovery/repeatability, and Release/non-functional for executable scientific components
→ include Component/Integration where they provide direct regression evidence
```

Higher level does not mean duplicating the same assertion in every category.

## Test-strength techniques

These improve evidence quality but are not standalone levels/categories and are not mandatory by default:

```text
coverage / branch coverage
property-based testing
fuzzing
mutation testing
fault injection
concurrency/race testing
benchmark/stress testing
```

Choose them when they attack a real risk:

- coverage identifies unexercised paths but does not prove correctness;
- mutation testing checks whether tests detect meaningful implementation changes;
- fault injection is valuable for filesystem/transaction/network failure boundaries;
- concurrency testing is justified only when concurrent access is supported or plausible;
- benchmark/stress testing is required only when performance/scale/resource claims are material.

Do not inflate test counts or percentages with redundant cases.

## Verification tools

Tools cover risks; installation alone never makes them mandatory.

### Semgrep

Use for targeted static/security analysis on meaningful attack or misuse surfaces such as path/filesystem handling, subprocess execution, untrusted parsing, serialization, network handling, authentication/authorization, secrets, or credentials.

### CodeQL

Use for deeper semantic/data-flow analysis when supported and justified by a release/security risk. Prefer an existing repository code-scanning workflow when available.

### pip-audit

Use for Python dependency-vulnerability evidence when dependency risk is in scope.

A tool finding is evidence to investigate, not automatic proof of a defect.

## Verification planning

### LOCAL-QUICK

LOCAL-QUICK normally uses LEVEL 1 and records only the focused evidence needed for ChatGPT acceptance review. A formal six-row matrix is not required.

### FORMAL

A formal task states:

```text
Verification level: LEVEL 1 | LEVEL 2 | LEVEL 3

Required evidence:
- <evidence category>: <concrete check/evidence>
- <evidence category>: <concrete check/evidence>
...
```

Only required categories are listed. Do not add `N/A` rows for irrelevant categories.

Write concrete evidence targets, for example:

```text
Real artifact / external tool: run one real MinerU PDF and inspect retained package
E2E / recovery / repeatability: induce parser failure, verify no partial final package, retry successfully
Release / non-functional risk: build wheel/sdist and install wheel into empty venv
```

## Reporting and acceptance

Codex reports what was actually executed for every evidence category required by the task, including failures, skips, environmental limitations, and material deviations from the plan.

A nominal `pytest PASS`, coverage percentage, scanner result, or CI badge does not substitute for a different required category.

ChatGPT acceptance review evaluates:

```text
was the verification level appropriate?
were the required evidence categories sufficient for the claim?
did the reported evidence actually establish those claims?
were limitations/deviations disclosed?
```

For LEVEL 2/3, add an independent reviewer/model/human perspective only when architecture, science, trust, security, or release risk warrants it; do not create reviewer ceremony by default.

## Summary

```text
LEVEL 1
→ focused, fast, directly relevant evidence

LEVEL 2
→ risk-driven multi-category evidence

LEVEL 3
→ release-claim-driven reproducibility and non-functional evidence

all levels
→ use only evidence categories and strengthening techniques that prove a real claim
```
