# Design reconciliation contract

Load this reference when keeping current Design synchronized with accumulated ChatGPT/Codex/Concept history.

## Purpose

Reports preserve what happened. Design preserves only the current accepted result.

```text
reports/chatgpt/ + reports/codex/ + reports/concept/
= append-only historical work/evidence

reports/design/
= mutable current accepted normal form
```

Do not wait for reconciliation when a Design consequence is already accepted. Update the owning Design topic in the same work unit.

## Project-local hook

Design reconciliation is not a background platform automation.

Every long-running project that uses `reports/design/` carries a short Design-maintenance hook in its root `AGENTS.md`.

When ChatGPT enters that project for substantive work:

```text
read AGENTS.md
→ read CURRENT.md
→ inspect the compact reconciliation cursor in reports/design/README.md
→ perform a cheap trigger check
→ if no trigger fires, continue current work without loading report history
→ if triggered, reconcile only reports newer than the cursor
→ then continue current work
```

If the project is not being worked on, nothing runs. No generic scheduler scans repositories in the background.

## Immediate synchronization

After ChatGPT accepts a task/result/discussion, ask:

```text
Did this work change an accepted project rule, interface, ownership boundary,
workflow/state contract, trust condition, runtime/Skill profile, or other Design concern?
```

If YES:

```text
update the owning reports/design topic(s) now
→ update reports/design/README.md only if routing/ownership changed
→ remove superseded current semantics
→ then continue
```

Execution detail, test output, branch mechanics, and historical rationale stay in Reports unless they establish a current rule.

## Opportunistic reconciliation triggers

At project entry, run bounded reconciliation when any condition is true since the last cursor:

```text
>= 4 new substantive reports across chatgpt + codex + concept
OR >= 7 days elapsed since reconciled_at
OR a new report declares design_signal: design_gap or design_drift
```

`reports/handoff/` does not count toward the report threshold.

The trigger check should be cheap. Use report filenames/metadata/cursor first; do not preload report bodies unless reconciliation actually triggers.

## Reconciliation cursor

`reports/design/README.md` carries compact maintenance metadata:

```yaml
design_reconciliation:
  reconciled_at: YYYY-MM-DD
  chatgpt_through: YYMMDD_chatgpt_NN | null
  codex_through: YYMMDD_codex_NN | null
  concept_through: YYMMDD_concept_NN | null
```

There is no `enabled` flag: a project that uses the standard `reports/design/` model also uses this maintenance check through its `AGENTS.md` hook.

This block is maintenance metadata only. It must not grow into a progress log.

## Reconciliation procedure

Read only reports newer than the cursor, then classify each Design-relevant delta:

```text
ACCEPTED_CURRENT_CHANGE
→ update the one current Design owner

EXECUTION_ONLY / EVIDENCE_ONLY / HISTORY_ONLY
→ no Design change

AMBIGUOUS_SCIENTIFIC_OR_PRODUCT_MEANING
→ do not infer; surface the exact decision to the User
```

Concept is historical reasoning, not automatic current authority. Use it as evidence for the accepted consequence; do not copy Concept prose wholesale into Design.

After every accepted current change is reflected, advance the cursor to the newest inspected report in each family.

## Topic-count guard

Healthy mature projects normally use roughly 5–8 current Design topics.

```text
adding topic 9+
→ first inspect whether ownership should merge

> 12 current topics
→ do not add another topic by default
→ perform Design consolidation first
→ exceeding the limit requires explicit User approval or a clearly independent responsibility
```

Existing complex projects above the threshold are not rewritten blindly, but further splitting is blocked until ownership is reviewed.

## Completion

Reconciliation is complete when every accepted Design-relevant delta in the inspected report window is represented by exactly one current Design owner, non-Design history remains in Reports, unresolved semantic choices are surfaced rather than guessed, and the cursor is advanced.
