# External tool integration contract

Load this reference only when a project integrates an external CLI, API, schema, parser, simulator, browser/runtime tool, or another independently evolving software interface.

## Adapter boundary

Third-party scientific/software tools use an explicit adapter boundary when their CLI, API, file layout, schema, or runtime behavior is implementation-specific and may evolve independently.

```text
project concept / contract
→ required capability and artifact semantics

owning adapter
→ concrete CLI/API/schema knowledge
→ version/profile compatibility checks
→ invocation and output discovery

other project modules
→ consume the adapter's project-facing result
→ do not duplicate third-party interface details
```

The project design layer defines required capability and artifact semantics. It should not unnecessarily freeze transient command spelling.

Concrete flags, endpoint paths, native output filename patterns, or schema branching should have one implementation owner. Duplicate external-interface knowledge only when a second occurrence is an intentionally bounded contract assertion.

## Known-profile verification

For an evolving external interface, prefer an explicit known-compatible profile plus verification over speculative runtime adaptation.

A probe may inspect stable surfaces such as:

```text
--version
--help
capability metadata
API version endpoint
schema/version marker
```

The probe verifies a known profile; it does not infer a new interface automatically.

If an expected capability changes in a way the adapter does not understand:

```text
unknown / semantically incompatible external profile
→ fail closed
→ report unsupported interface
→ update + revalidate adapter explicitly
```

Do not guess renamed flags, select merely plausible replacements, silently switch tools/backends, or reinterpret changed semantics because an invocation happens to run.

## Scientific reproducibility

For result-bearing scientific tools, successful execution alone is not evidence of semantic compatibility.

Record tool/version/configuration facts that materially affect reproducibility when those facts are part of result provenance.

Exact version pinning is not universal:

```text
exact-environment reproduction
→ fixed version/profile may be required

validated compatible operating range
→ known compatible profile may be sufficient
```

In both cases, reproducibility and explicit semantics outrank speculative forward compatibility.

## Unknown-interface behavior

When the external tool cannot be reconciled with a validated profile, stop at the adapter boundary rather than leaking guessed compatibility into project semantics.

Do not let an external tool's success exit code redefine scientific/product correctness.

## Relationship to prior art

When choosing a new substantial external framework/tool, the project prior-art gate may also apply. `SKILL.md` routes that design concern directly to `prior-art.md`; do not load it for routine invocation of an already accepted adapter.
