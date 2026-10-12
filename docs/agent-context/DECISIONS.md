# Durable decisions

## Confirmed decisions
1. **This is supporting GAL validation work, not a separate marketed product.** Reason: describe its role accurately. Source: the repository's [runtime-only structure](../../runtime/), reviewed on 2026-10-11. “GAL · Codex Validation” is a descriptive portfolio label.
2. **Preserve GAL v0.5.0 as the reviewed runtime baseline.** Reason: an isolated evaluation must not silently change the subject being evaluated. Sources: [runtime README](../../runtime/README.md), [Core version](../../runtime/steering/gal-core.md), and [configuration template](../../runtime/templates/config.json).
3. **GAL Core governs semantics; canonical adapters govern host mechanics.** Reason: preserve methodology across hosts. Sources: [root loader](../../AGENTS.md) and [Host Adapter Contract](../../runtime/contracts/HOST-ADAPTER-CONTRACT.md).
4. **Canonical GAL state is JSON; generated context is refreshed through runtime sync.** Reason: preserve one writable state authority. Sources: [Core](../../runtime/steering/gal-core.md), [runtime README](../../runtime/README.md), and [Codex adapter](../../runtime/adapters/codex/AGENTS.md). This contributor context directory is not a second GAL state store.
5. **Blind evaluation excludes regression answers and prior results.** Reason: maintain valid host evaluation. Sources: [runtime isolation rules](../../runtime/README.md) and [Host Adapter Contract](../../runtime/contracts/HOST-ADAPTER-CONTRACT.md).
6. **Unavailable execution cannot count as successful validation.** Reason: preserve execution truth. Sources: [Core](../../runtime/steering/gal-core.md) and [canonical adapter](../../runtime/adapters/codex/AGENTS.md).

## Open decisions
- A future baseline upgrade or additional host evaluation needs an explicit scope and separate evaluator record. No upgrade or new conformance claim is established by this documentation rollout.

## Recording rules
Record only confirmed durable choices with date, reason, authority, and source. Keep pending ideas open, preserve historical evidence, and link the underlying contract or design. Do not copy secrets, customer data, blind-test inputs, expected answers, grading criteria, transcripts, or prior results into these context files. GAL state and Core remain authoritative for GAL-managed work.
