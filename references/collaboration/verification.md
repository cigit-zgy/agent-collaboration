# Verification contract

Verification has two dimensions:

```text
level    = how much rigor/cost the task warrants
category = what evidence is needed for the specific claim
```

A task selects one level and only the evidence categories material to its risks. Categories are not a second level system and need not all appear.

## Levels

### LEVEL 1 — FOCUSED

Default for ordinary development and LOCAL-QUICK.

Use directly affected tests/checks, relevant lint/type checks, and the smallest useful smoke/integration evidence. Optimize for fast feedback.

### LEVEL 2 — MAJOR

Use for core architecture, scientific/product behavior, important public contracts, trust boundaries, or material cross-module changes.

Add only risk-relevant evidence such as stronger contract/integration checks, real artifacts, recovery behavior, targeted security/static analysis, or an additional adversarial review perspective.

### LEVEL 3 — RELEASE

Use for release qualification, open-source/release readiness, or security-sensitive release gates.

Cover the reproducibility and non-functional evidence required by the actual release claim: packaging/install, environment matrix, dependencies, static/security, real artifacts, recovery/repeatability, and similar concerns when material.

LEVEL 3 does not mean every available test or scanner.

## Evidence categories

### Component / property

Small deterministic behavior and local invariants.

```text
focused tests
boundary/parameterized cases
pure-function checks
property/fuzz tests when input-space risk warrants them
```

### Contract / invariant

Stable public/project-facing behavior independent of implementation details.

```text
schema/fields
file ownership
state transitions
trust boundaries
CLI/API behavior
fail-closed conditions
serialization/provenance
```

Avoid self-proof where practical: critical expected invariants should not be derived only from the same production constant/code path being tested.

### Integration

Interactions among in-scope components or adjacent boundaries.

```text
component → component
CLI → implementation
registry → consumer
adapter → orchestrator
synthetic stage handoff
```

### Real artifact / external tool

Behavior that mocks/synthetic inputs cannot establish reliably.

```text
real scientific PDF/data/model
real parser/simulator/tool
real package/resource layout
representative domain edge case
```

Reuse stable expensive artifacts when fresh reconstruction adds no evidence.

### E2E / recovery / repeatability

Complete in-scope flow and adverse transitions when material.

```text
fresh input → stable result
failure → no partial authoritative state
retry/idempotency
independent reconstruction/repeatability
```

Keep E2E sparse; lower-cost evidence should prove lower-level properties.

### Release / non-functional risk

Evidence that a release claim survives outside the current worktree/happy path.

```text
build + clean/non-editable install
package self-containment
supported runtime/OS matrix
dependency/static/security checks
performance/scale limits when claimed
repository/open-source/status-gate readiness
```

Do not invent irrelevant non-functional tests to fill the category.

## Level guidance

```text
LEVEL 1
→ Component/property by default
→ add Contract/Integration when touched
→ higher-cost categories only when directly implicated

LEVEL 2
→ affected Component/Contract/Integration
→ Real artifact when scientific/tool reality matters
→ E2E/recovery/repeatability for trust/transaction/full-flow risk
→ Release/non-functional only for concrete risk

LEVEL 3
→ every category material to the release claim
→ commonly Contract + Real artifact + E2E/recovery/repeatability + Release/non-functional for executable scientific components
```

Do not duplicate the same assertion across categories merely to increase evidence volume.

## Strengthening techniques

These are optional techniques inside the relevant category, not levels/categories themselves:

```text
coverage / branch coverage
property testing / fuzzing
mutation testing
fault injection
concurrency/race testing
benchmark/stress testing
```

Use them only against a real risk. Coverage finds unexercised paths but is not correctness; mutation testing tests test sensitivity; fault injection is valuable at failure boundaries; concurrency tests require plausible concurrent access; benchmarks require a performance/scale claim.

## Security/dependency tools

Select by risk:

```text
Semgrep  → targeted source/static security analysis
CodeQL   → deeper semantic/data-flow analysis when justified and supported
pip-audit→ Python dependency-vulnerability evidence
```

Tool installation does not make a tool mandatory, and a finding is evidence to investigate rather than automatic proof of a defect.

## Planning

LOCAL-QUICK normally uses LEVEL 1 and records only the focused evidence needed for acceptance review.

A FORMAL task states:

```text
Verification level: LEVEL 1 | LEVEL 2 | LEVEL 3

Required evidence:
- <category>: <concrete check>
- <category>: <concrete check>
```

List only required categories; do not add `N/A` rows.

Example:

```text
Verification level: LEVEL 2
Required evidence:
- Contract / invariant: registry schema + fail-closed path checks
- Real artifact / external tool: real MinerU PDF retained-artifact check
- E2E / recovery / repeatability: parser failure leaves no partial final package; retry succeeds
```

## Reporting and acceptance

Codex reports what actually ran for each required category, including failures, skips, environment limits, and plan deviations.

A `pytest PASS`, coverage number, scanner result, or CI badge does not substitute for another required evidence category.

ChatGPT acceptance review asks whether the chosen level and evidence were sufficient and whether the evidence establishes the claim. Add a second reviewer/model/human perspective for LEVEL 2/3 only when scientific, architectural, trust, security, or release risk materially warrants it.
