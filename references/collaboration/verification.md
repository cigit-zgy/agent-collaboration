# Verification contract

Load this reference when deciding how much verification a change needs or where that evidence should run.

## Core rule

Verification is proportional to the claim and risk.

```text
small reversible change
→ focused affected checks

material contract or scientific change
→ stronger contract/integration/real-artifact evidence

release-critical change
→ release-level evidence appropriate to the actual claim
```

Do not broaden or repeat testing merely to increase evidence volume. Once required checks pass, continue toward completion unless new changes, failures, or unresolved concerns justify more work.

## Levels

### LEVEL 1 — FOCUSED
Default for ordinary development and LOCAL-QUICK. Run directly affected checks plus the smallest useful smoke/integration evidence when needed.

### LEVEL 2 — MAJOR
Use for important architecture, scientific/product behavior, public contracts, or trust boundaries. Add only the stronger evidence the changed claim actually needs.

### LEVEL 3 — RELEASE
Use for release qualification. Verify the properties required by the release claim, such as packaging/installability, supported environments, representative real artifacts, recovery/repeatability, and material dependency/static checks.

LEVEL 3 does not mean “run every available test”.

## Placement

Use connected ChatGPT verification when the required check is already available cheaply online.

Use Codex/local verification when evidence depends on the User machine, project runtime, native dependencies, local services, browser automation, hardware, proprietary data, large builds, or long-running execution.

Do not duplicate an expensive check in two places unless the second environment proves a distinct property.

## Meaningful tests

Prefer checks that establish a real behavior, boundary, invariant, failure mode, or integration property.

Avoid tests that merely mirror implementation for a reversible low-impact change. Astra-class coding agents already tend to test thoroughly; instructions should keep verification from becoming a second implementation project.

## Evidence selection

When relevant, evidence may include:

```text
focused component/property checks
contract or invariant checks
integration checks
representative real-artifact/tool runs
failure/recovery/repeatability checks
release/non-functional checks
```

Select only what the task needs. Do not add `N/A` categories or redundant assertions.

## Task planning

A task should state only:

```text
Verification level: LEVEL 1 | LEVEL 2 | LEVEL 3
Required evidence:
- <concrete checks needed for the claim>
```

If ChatGPT already established a claim and later changes did not invalidate it, Codex need not repeat it unless local confirmation proves a distinct property.

## Reporting

Record what actually ran, material failures/skips/limitations, and whether the requested completion claim is established.
