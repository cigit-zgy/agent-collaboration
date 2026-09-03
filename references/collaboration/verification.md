# Verification contract

Verification has two orthogonal dimensions:

```text
verification level
= how much rigor/cost the current task warrants

verification evidence layer
= at what system scale the required evidence is collected
```

A formal Codex task selects exactly one verification level and then selects only the evidence layers materially required by the task's risks and acceptance claim.

The three levels are not test types. The six evidence layers are not a second level system. A LEVEL 3 task is therefore not automatically "run every possible test"; it must cover every evidence layer that is material to the release claim and explicitly mark genuinely inapplicable layers as such.

## Verification levels

### LEVEL 1 — FOCUSED

Default for ordinary development, one Skill/reference, small bugs, and small or medium implementations.

Evidence normally includes directly affected tests/checks, relevant lint/type checks for touched code, the smallest useful smoke/integration check, and ChatGPT independent audit.

### LEVEL 2 — MAJOR

Use when a task changes core architecture, scientific/product logic, a trust boundary, or important cross-module behavior.

Level 2 adds only evidence required by that risk, such as affected contract/integration checks, real-artifact validation, recovery/failure behavior, a materially useful independent second perspective, or targeted static/security analysis.

### LEVEL 3 — RELEASE

Use for formal release, component release qualification, open-source readiness, or security-sensitive release gates.

Level 3 adds release/reproducibility evidence and the packaging, clean-install, environment, dependency, static/security, real-artifact, recovery, repeatability, and audit evidence required by the specific release target.

## Verification evidence layers

The following six layers describe *where* evidence is collected. They complement rather than replace the three verification levels.

### LAYER 1 — Component / property

Checks small deterministic behavior and local invariants close to the implementation unit.

Typical evidence includes:

```text
focused pytest
pure-function checks
boundary-value cases
parameterized cases
property-based or fuzz tests when input-space risk warrants them
```

Use property/fuzz testing when many valid/invalid combinations matter more than a few hand-written examples. It is a technique inside this layer, not a universal requirement.

### LAYER 2 — Contract / invariant

Checks that stable public/project-facing behavior matches the accepted contract independently of implementation details.

Typical targets include:

```text
schemas and exact fields
file/directory ownership
state-transition rules
trust-boundary invariants
stable CLI/API behavior
fail-closed conditions
serialization and provenance rules
```

Critical contract tests should avoid self-proof where possible: expected invariants should not be derived solely from the same production constants or code paths being tested.

### LAYER 3 — Integration

Checks interactions among multiple components inside one Skill/module or across explicitly in-scope adjacent boundaries.

Typical evidence includes:

```text
component A → component B
CLI → implementation
registry → consumer
adapter → orchestrator
synthetic stage-to-stage filesystem handoff
```

Prefer small deterministic fixtures so interface failures remain diagnosable.

### LAYER 4 — Real-artifact regression

Checks the implementation against real scientific/domain artifacts or real external tools when mocks/synthetic inputs cannot represent the important behavior.

Typical evidence includes:

```text
real PDFs/data/model files
real parser/simulator/tool execution
real package/resource layouts
representative domain-specific edge cases
```

Reuse stable real artifacts when upstream behavior has not changed; rerun expensive upstream work only when the task needs fresh reconstruction evidence.

### LAYER 5 — End-to-end / recovery / repeatability

Checks the complete in-scope user-visible or trust-boundary flow from a fresh starting state to the stable result, including adverse transitions when they materially matter.

Typical evidence includes:

```text
fresh source → final in-scope artifact
failure → no partial authoritative state
retry/recovery
idempotent reuse
independent fresh reconstructions
cross-run integrity/repeatability
```

End-to-end evidence is intentionally sparse. Do not move every lower-level case into E2E merely for reassurance.

### LAYER 6 — Release / non-functional

Checks whether the release claim remains valid outside the developer's current worktree and happy-path runtime.

Select the relevant release risks, for example:

```text
clean wheel/sdist or equivalent build
non-editable clean installation
package self-containment
supported OS/Python/runtime matrix
dependency vulnerability audit
static/security analysis
performance/scale/resource limits when claimed
open-source/repository readiness
branch/status-gate behavior when part of release governance
```

A release task does not need irrelevant non-functional tests. For example, do not invent load testing for a local file converter that makes no throughput claim.

## Level × layer selection

Use risk, not ceremony.

```text
LEVEL 1
→ normally Layer 1
→ add Layer 2/3 when the touched behavior exposes a contract/interface
→ Layers 4–6 only when directly implicated

LEVEL 2
→ include affected Layer 1–3 evidence
→ add Layer 4 when real scientific artifacts/external tools matter
→ add Layer 5 when a trust boundary, transaction, recovery, or cross-stage flow changes
→ add Layer 6 only for a concrete non-functional/security/dependency risk

LEVEL 3
→ cover every layer materially required by the release claim
→ normally includes Layers 2, 4, 5, and 6 for executable scientific components
→ include Layer 1/3 where they provide direct regression evidence
→ explicitly state N/A for any omitted layer whose absence could otherwise be ambiguous
```

Higher verification level does not mean duplicating the same assertion at every layer. Prefer the lowest layer that proves a property, then add higher-layer evidence only for behavior that emerges from integration, real artifacts, full flow, or release environment.

## Test-strength techniques

The following techniques improve evidence quality but are not standalone verification layers and are not automatically mandatory:

```text
coverage measurement
branch coverage
property-based testing
fuzzing
mutation testing
fault injection
concurrency/race testing
benchmark/stress testing
```

Select them when they attack a real risk:

- coverage identifies unexercised code paths but does not by itself prove correctness;
- mutation testing checks whether tests actually detect meaningful implementation changes;
- fault injection is high-value for transactional/filesystem/network failure boundaries;
- concurrency testing is justified only when concurrent access is supported or plausible;
- benchmarks/stress tests are required only when performance, scale, or resource limits are part of the claim.

Do not inflate test counts or coverage percentages with redundant cases merely to reach a number.

## Verification tools

Verification tools cover a defined risk; installation alone never makes a tool mandatory.

### Semgrep

Use as a fast static/security layer for meaningful attack or misuse surfaces such as filesystem/path handling, subprocess execution, network input, untrusted parsing, serialization, authentication, authorization, secrets, or credential handling.

Typical targeted use:

```text
semgrep scan --config auto <TARGET>
```

### CodeQL

Use for deeper semantic/data-flow analysis when supported, permitted, and justified by an explicit security/release risk. Prefer an existing repository code-scanning workflow when available.

### pip-audit

Use for Python dependency-vulnerability coverage when dependency risk is in scope.

## Formal task verification plan

A formal task's `## Verification` section must state:

```text
Verification level: LEVEL 1 | LEVEL 2 | LEVEL 3

Evidence-layer plan:
- Layer 1 — Component/property: required | N/A — <reason>
- Layer 2 — Contract/invariant: required | N/A — <reason>
- Layer 3 — Integration: required | N/A — <reason>
- Layer 4 — Real-artifact regression: required | N/A — <reason>
- Layer 5 — E2E/recovery/repeatability: required | N/A — <reason>
- Layer 6 — Release/non-functional: required | N/A — <reason>
```

For each required layer, name the concrete evidence expected rather than merely repeating the layer title.

The task author may group clearly related checks, but the intended coverage must remain auditable.

## Reporting and acceptance

Codex reports what was actually executed under each required layer, including failures, skips, environmental limitations, and deviations from the planned evidence.

A nominal `pytest PASS` does not substitute for a missing real-artifact, E2E, recovery, or release layer when the task required that evidence.

Likewise, a failed out-of-scope repository-wide check does not automatically invalidate an in-scope layer if the task explicitly separates that downstream drift and the current acceptance claim does not include it.

ChatGPT independently evaluates whether the selected level was appropriate, whether the layer plan matched the task risk, and whether the reported evidence actually supports the acceptance verdict.

## Selection summary

```text
LEVEL 1
→ focused evidence; no adversarial scanner by default

LEVEL 2
→ risk-driven multi-layer evidence
→ Semgrep when attack/misuse surface warrants it
→ CodeQL only for justified deep security analysis
→ pip-audit when dependency risk is in scope

LEVEL 3
→ release-claim-driven evidence across all materially relevant layers
→ select source/dependency/security/reproducibility tools according to release risk
```

Machine-wide developer tools remain separate from project runtime dependencies. A tool finding is evidence to investigate, not automatic proof of a defect.

A clean environment rebuild is verification only when environment reproducibility is itself under test, the current environment is invalid, or a release gate requires it.
