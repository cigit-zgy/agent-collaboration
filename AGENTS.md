# agent-collaboration repository context

## Identity

This repository is the maintained first-party source for the `agent-collaboration` Skill.

## Authority

```text
AGENTS.md
= repository-maintenance constitution

SKILL.md
= runtime routing index

references/
= current operational owners

reports/concept/
= historical collaboration reasoning only
```

User + ChatGPT maintain collaboration design. The User retains final decision/override authority. ChatGPT performs connected DIRECT authoring and acceptance review. Codex executes approved LOCAL work and does not self-accept.

## Owner map

```text
references/collaboration/protocol.md   roles / authority / refresh / trust
references/collaboration/execution.md  DIRECT/LOCAL/FORMAL + Git/worktree/tmp/sync
references/collaboration/formal.md     FORMAL lifecycle/acceptance/integration
references/project/governance.md       project artifact admission + conformance gate
references/project/current.md          CURRENT.md + normal multi-conversation resume
references/project/migration.md        existing-project collaboration migration
references/project/reports.md          reports/design + chronological report layout
references/project/concept.md          explicit User-requested Concept history
references/project/design.md           current living Design under reports/design/
references/project/prior-art.md        external prior-art/reuse gate
references/project/handoff.md          exceptional conversation-only delta
references/skill/development.md        Design → Skill Markdown → implementation → tests
```

Read `SKILL.md` first and load only the owning reference.

## Hard invariants

- Before the first substantive repository-changing ChatGPT write in a work unit, apply the bounded project governance conformance gate when project governance surfaces are implicated.
- Deterministic governance drift is corrected before new work expands it; scientific/product/design ambiguity returns to User + ChatGPT.
- `reports/design/` is the only current living-design tree when explicit Design is used.
- Every current design concern has one owner. A current topic must not remain merely as a superseded/refining/overriding alternative to another current owner.
- A bounded design concern should normally require one primary current owner plus at most one necessary secondary owner; persistent three-plus-owner reading chains are `DESIGN_ARCHITECTURE_DRIFT`.
- ChatGPT does not create `reports/concept/` artifacts unless the User explicitly requests Concept persistence.
- Every normal Concept persistence request creates a new dated Concept artifact; existing Concepts are not overwritten.
- The same work unit that creates a requested Concept also updates current `reports/design/` to the accepted consequence.
- Concept is append-only history; Design is mutable current state and replaces/merges/removes superseded current owners.
- Scientific/model facts, qualification evidence, test results, and execution records stay with their scientific/task/report owners rather than being routed to Concept or project Design by convenience.
- Long-running projects use root `CURRENT.md` only for NOW-state/work edge; target <=4 KiB and >8 KiB is non-conforming without explicit project justification.
- Normal conversation resume is `AGENTS.md → CURRENT.md → reports/design/README.md`, not project migration and normally not handoff.
- Every Codex repository task is committed under `reports/chatgpt/` before delegation; chat contains only the locator.
- LOCAL-QUICK creates no `reports/codex/` report; FORMAL does.
- Every repository-changing Codex task fresh-fetches before mutation and after push and proves exact local/authorized-remote equality at both boundaries.
- Historical reports/templates/archive are cold unless directly needed.
- Skill behavior changes follow `reports/design/ → SKILL.md/references → implementation → design-probing tests`.
