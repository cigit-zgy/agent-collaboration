# agent-collaboration repository context

This repository maintains the `agent-collaboration` Skill.

## Authority

```text
User instruction
→ AGENTS.md                       repository-maintenance constitution
→ SKILL.md                        runtime router
→ references/                     current operational owners
→ reports/concept/                historical collaboration reasoning only
```

User + ChatGPT maintain collaboration design. Codex executes authorized local work and never self-accepts.

## Owner map

```text
references/collaboration/protocol.md   roles, precedence, decision boundaries
references/collaboration/execution.md  DIRECT/LOCAL-QUICK/FORMAL + local-state safety
references/collaboration/formal.md     FORMAL lifecycle and acceptance
references/collaboration/verification.md risk-proportional evidence
references/project/governance.md       generic project artifact admission / drift
references/project/current.md          CURRENT.md + conversation resume
references/project/design.md           current living Design
references/project/concept.md          explicit User-requested Concept history
references/project/migration.md        existing-project migration
references/skill/development.md        Design → Skill → implementation → tests
references/skill/writing.md            Skill trigger/routing/progressive disclosure
```

Read `SKILL.md` first and load only the owner required by the active concern.

## Hard boundaries

- Explicit User instructions take precedence over generic collaboration guidance.
- Routine reversible engineering proceeds autonomously inside the authorized scope; ask only at a real scientific/product, destructive, security/permission, public/release, or explicit User checkpoint.
- Project-specific scientific facts and canonical-artifact rules stay in the project that owns them; do not promote them into generic collaboration policy.
- `reports/design/` is current state; `reports/concept/` is historical and created only when the User explicitly requests Concept persistence.
- Codex repository work uses a committed `reports/chatgpt/` task; chat is only the locator.
- Verification is proportional to the claim and risk; do not broaden or repeat checks without a concrete reason.
