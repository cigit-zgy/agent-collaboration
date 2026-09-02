# Verification tools

Use verification tools to cover a defined risk. Do not install or run them merely
because they exist. The formal task and `verification-levels.md` decide when the
extra cost is justified.

## Primary adversarial/static tools

### Semgrep Community Edition

Use Semgrep as the fast first security/static-analysis layer when changed code
includes a meaningful attack or misuse surface, such as:

- filesystem/path handling;
- subprocess or shell execution;
- network or HTTP handling;
- parsing of untrusted input;
- serialization/deserialization;
- authentication, authorization, secrets, or credential handling.

Typical use:

```text
semgrep scan --config auto <TARGET>
```

Prefer a narrower target over scanning unrelated repositories. Level 1 does not run
Semgrep by default. Use it for targeted security-sensitive Level 2 work or Level 3
when relevant.

### CodeQL

Use CodeQL for deeper semantic/data-flow analysis where supported and available.
It is primarily a Level 3 release/security gate, or an explicitly security-sensitive
Level 2 task whose risk justifies deeper analysis.

Prefer the repository's existing GitHub code-scanning workflow when one exists.
Otherwise use the supported CodeQL CLI/workflow for the repository language and
selected query suite. Do not make CodeQL availability a universal development
requirement.

## Python dependency audit

### pip-audit

For Python release/security work, use `pip-audit` when dependency vulnerability
coverage is relevant. It complements source-code analysis; it does not replace
Semgrep/CodeQL or project tests.

Do not run dependency audits on every ordinary implementation task.

## Selection by verification level

```text
LEVEL 1 — FOCUSED
→ no adversarial scanner by default

LEVEL 2 — MAJOR
→ Semgrep only when the changed attack/misuse surface justifies it
→ CodeQL only for explicitly security-sensitive deep analysis
→ pip-audit only when dependency risk is in scope

LEVEL 3 — RELEASE
→ select Semgrep and/or CodeQL according to language and repository risk
→ add pip-audit for Python dependency release gates when applicable
```

A tool finding is evidence to investigate, not automatic proof of a defect. Record
material findings and disposition in the Codex report. Do not create extra scanner
artifacts or permanent configuration unless the repository has a current consumer
for them.
