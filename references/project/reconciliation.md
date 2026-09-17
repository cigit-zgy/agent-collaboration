# Design reconciliation contract

Load this reference when keeping current Design synchronized with accumulated ChatGPT/Codex/Concept history, or when configuring a periodic Design-maintenance check.

## Purpose

Reports preserve what happened. Design preserves only the current accepted result.

```text
reports/chatgpt/ + reports/codex/ + reports/concept/
= append-only historical work/evidence

reports/design/
= mutable current accepted normal form
```

Do not wait for periodic reconciliation when a design consequence is already accepted. Update the owning Design topic in the same work unit.

## Immediate synchronization

After ChatGPT accepts a task/result/discussion, ask one question:

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

Execution detail, test output, branch mechanics, and historical rationale stay in Reports and do not enter Design unless they establish a current rule.

## Backstop reconciliation triggers

Run a bounded reconciliation when any condition is true since the last reconciliation cursor:

```text
>= 4 new substantive reports across chatgpt + codex + concept
OR >= 7 days elapsed
OR any new report carries DESIGN_GAP or DESIGN_DRIFT
```

`reports/handoff/` does not count toward the report threshold.

For active long-running projects, a useful scheduled backstop is three checks per week. The scheduled check is not a substitute for immediate synchronization.

## Reconciliation cursor

`reports/design/README.md` may carry a compact maintenance block:

```yaml
design_reconciliation:
  reconciled_at: YYYY-MM-DD
  chatgpt_through: YYMMDD_chatgpt_NN | null
  codex_through: YYMMDD_codex_NN | null
  concept_through: YYMMDD_concept_NN | null
```

This is maintenance metadata only. It does not add Design semantics and must not grow into a progress log.

## Reconciliation procedure

Read only reports newer than the cursor, then classify each design-relevant delta:

```text
ACCEPTED_CURRENT_CHANGE
→ update the one current Design owner

EXECUTION_ONLY / EVIDENCE_ONLY / HISTORY_ONLY
→ no Design change

AMBIGUOUS_SCIENTIFIC_OR_PRODUCT_MEANING
→ do not infer; surface the exact decision to the User
```

After all accepted current changes are reflected, advance the cursor to the newest inspected report in each family.

Do not summarize reports wholesale into Design. Design must remain current-state prose, not a digest.

## Topic-count guard

Healthy mature projects normally use roughly 5–8 current Design topics.

```text
adding topic 9+
→ first inspect whether ownership should merge

> 12 current topics
→ do not add another topic by default
→ perform Design consolidation first
→ exceeding the limit requires explicit User approval or a documented independent responsibility that cannot be merged cleanly
```

Existing complex projects above the threshold are not rewritten blindly, but further splitting is blocked until ownership is reviewed.

## Completion

Reconciliation is complete when every accepted design-relevant delta in the inspected report window is represented by exactly one current Design owner, non-design history remains in Reports, unresolved semantic choices are surfaced rather than guessed, and the reconciliation cursor is advanced.
