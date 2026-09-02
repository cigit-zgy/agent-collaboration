# Verification levels

Every ChatGPT formal task specifies exactly one level. `LEVEL 1 — FOCUSED` is the
default for ordinary development. Codex performs the selected level and does not
upgrade it on its own unless it discovers a concrete security or data-loss risk;
any such escalation must be explained in the Codex report.

Verification effort is proportional to the current risk. Optimize for fast feedback
during development; reserve broad validation for tasks that actually need it.

## LEVEL 1 — FOCUSED

Use for local changes, one Skill or reference, small bugs, and ordinary small or
medium implementations.

- directly affected tests and checks;
- Ruff or mypy only when relevant to touched Python;
- the smallest real smoke/integration check needed for the changed flow;
- ChatGPT independent audit.

Do not automatically run the full repository test suite, rebuild a clean
environment, reinstall all dependencies, launch multiple reviewers, or perform
release/security scanning for Level 1.

## LEVEL 2 — MAJOR

Use only when the task explicitly changes core architecture, core scientific or
product logic, a trust boundary, or important cross-module behavior.

Level 2 includes Level 1 plus only the broader evidence required by the affected
risk:

- affected integration tests;
- necessary end-to-end or real-artifact validation;
- an independent second perspective when it can materially test the design;
- targeted security/static analysis when the changed surface is security-sensitive.

The second perspective may be another Agent critique, an alternative
implementation review, or an explicit adversarial review. Do not create multiple
Agents merely for ceremony. Do not rebuild an environment merely to prove
cleanliness unless environment reproducibility is itself under test or the current
environment is demonstrably invalid.

## LEVEL 3 — RELEASE

Use only for a formal release, open-source readiness, or a security-sensitive
release gate.

Level 3 includes Level 2 plus, as applicable:

- repository-audit;
- open-sourcing;
- dependency and static/security analysis;
- release checks and reproducibility evidence required by the release target.

Even at Level 3, use tools because they cover a defined risk or release gate, not
because more checks appear safer.
