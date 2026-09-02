# Verification contract

Verification effort follows the risk of the current task. Every formal Codex task selects exactly one level.

## LEVEL 1 — FOCUSED

Default for ordinary development, one Skill/reference, small bugs, and small or medium implementations.

Evidence normally includes directly affected tests/checks, relevant lint/type checks for touched code, the smallest useful smoke/integration check, and ChatGPT independent audit.

## LEVEL 2 — MAJOR

Use when a task changes core architecture, scientific/product logic, a trust boundary, or important cross-module behavior.

Level 2 adds only evidence required by that risk, such as affected integration/E2E checks, real-artifact validation, a materially useful independent second perspective, or targeted static/security analysis.

## LEVEL 3 — RELEASE

Use for formal release, open-source readiness, or security-sensitive release gates.

Level 3 adds release/reproducibility evidence and the repository-audit, open-sourcing, dependency, static, or security checks required by the release target.

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

## Selection summary

```text
LEVEL 1
→ no adversarial scanner by default

LEVEL 2
→ Semgrep when attack/misuse surface warrants it
→ CodeQL only for justified deep security analysis
→ pip-audit when dependency risk is in scope

LEVEL 3
→ select source/dependency/security tools according to release risk and repository eligibility
```

Machine-wide developer tools remain separate from project runtime dependencies. A tool finding is evidence to investigate, not automatic proof of a defect.

A clean environment rebuild is verification only when environment reproducibility is itself under test, the current environment is invalid, or a release gate requires it.
