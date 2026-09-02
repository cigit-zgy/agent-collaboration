# Verification levels

Every ChatGPT formal task specifies exactly one level. Codex performs that level
and does not upgrade it on its own unless it discovers a concrete security or
data-loss risk; any such escalation must be explained in the Agent report.

Verification effort is proportional to the current risk.

## LEVEL 1 — FOCUSED

Use for local changes, one Skill or reference, small bugs, and small
implementations.

- directly affected tests and checks;
- Ruff or mypy only when relevant to touched Python;
- ChatGPT independent audit.

Do not automatically expand Level 1 into full-repository or release validation.

## LEVEL 2 — MAJOR

Use for core architecture, core scientific logic, and important cross-module
changes.

Level 2 includes Level 1 plus:

- affected integration tests;
- necessary end-to-end or real-artifact validation;
- an independent second perspective when useful.

The second perspective may be another Agent critique, an alternative
implementation review, or an explicit adversarial review. Do not create
multiple Agents merely for ceremony.

## LEVEL 3 — RELEASE

Use only for a formal release, open-source readiness, or a security-sensitive
release gate.

Level 3 includes Level 2 plus:

- repository-audit;
- open-sourcing;
- appropriate static or security analysis, such as CodeQL when applicable;
- release checks.
