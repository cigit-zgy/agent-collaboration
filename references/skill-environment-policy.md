# Skill environment policy

Do not create one environment per Skill by default. Environment ownership follows
what actually executes code.

## Documentation-only Skill

A Skill containing only `SKILL.md`, references, templates, or other instruction
assets owns no runtime environment.

Do not create `.venv`, Conda environments, dependency locks, or package metadata
solely because the Skill exists.

## Skill used inside a project runtime

When a Skill guides code that runs inside a project, use the project's declared
environment and toolchain. The project repository remains the authority for Python
version, dependencies, package manager, Conda/venv policy, and test commands.

Do not create a parallel Skill-specific environment for the same project runtime.

## First-party Skill with executable code

A first-party Skill that contains independently executable code may declare its own
runtime/toolchain when there is a real consumer. Prefer the smallest conventional
project declaration, such as `pyproject.toml` for Python.

Create or rebuild an environment only when required to execute that code, repair an
invalid environment, or test environment/release reproducibility.

Ordinary code changes should reuse a healthy existing environment.

## Third-party Skill

Follow upstream installation/runtime instructions. Do not mutate the upstream
Skill's environment model, vendor dependencies, or create a new environment unless
installation or the active task requires it.

## Verification discipline

A clean environment rebuild is not a default verification technique. Use one only
when:

- environment reproducibility is the thing being tested;
- the existing environment is missing, corrupted, or demonstrably inconsistent;
- a release gate explicitly requires a clean install.

Report any environment creation, deletion, rebuild, or dependency mutation that was
necessary for a task. Do not delete or replace a user's environment merely to make
verification look cleaner.
