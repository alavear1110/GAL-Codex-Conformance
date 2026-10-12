# Project context

## Identity
- Display name: **GAL · Codex Validation** — supporting validation work for GAL Labs / GAL Method, not a separate marketed product.
- Repository: `alavear1110/GAL-Codex-Conformance`; default branch: `main`.
- Retain the repository slug and GAL v0.5.0 baseline identifiers; the display name does not rename internal artifacts.

## Purpose and users
This repository holds an isolated runtime used to evaluate GAL through the Codex reference host. It gives the evaluator access to runtime instructions and tools while keeping regression fixtures and expected answers outside the test environment.

## Architecture and entry points
- The [root loader](../../AGENTS.md) points to [GAL Core](../../runtime/steering/gal-core.md) and the [Codex adapter](../../runtime/adapters/codex/AGENTS.md).
- The [runtime](../../runtime/gal.ps1), schemas, steering, contracts, and templates form the reviewed v0.5.0 baseline. The [Kiro adapter](../../runtime/adapters/kiro/KIRO.md) is also present; presence alone does not establish a conformance result.
- The [Host Adapter Contract](../../runtime/contracts/HOST-ADAPTER-CONTRACT.md) defines the boundary between Core and host execution.
- Initialized projects write canonical state to `.gal/state/project-state.json` and generate `.gal/context/*` via runtime sync. Neither state path is committed in this snapshot.
- Repository-context documents are an orientation index. They do not replace GAL state, alter runtime semantics, or introduce a new baseline.

## Working agreements
Preserve the isolated runtime-only baseline. Keep blind-test scenarios, expected answers, grading criteria, transcripts, and prior results outside this repository and unavailable to a host undergoing a blind run. Do not silently upgrade this v0.5.0 copy to GAL Labs' newer baseline.

Load GAL Core and the canonical adapter before GAL-managed requirements work. Persist tracked questions in canonical state, preserve vocabulary and evidence rules, and refresh generated views through the runtime. Never directly edit `.gal/context/*`, bypass PowerShell trust controls, or claim successful execution or validation without observed success. Generic provider context entrypoints only help discover repository instructions; they do not implement or certify GAL host adapters.

## Source map
- [Root loader](../../AGENTS.md), [runtime README](../../runtime/README.md)
- [GAL Core](../../runtime/steering/gal-core.md), [steering phases](../../runtime/steering/)
- [Codex adapter](../../runtime/adapters/codex/AGENTS.md), [Kiro adapter](../../runtime/adapters/kiro/KIRO.md)
- [Host Adapter Contract](../../runtime/contracts/HOST-ADAPTER-CONTRACT.md), [adapter schema](../../runtime/contracts/adapter.schema.json)
- [State schema](../../runtime/schemas/project-state.schema.json), [runtime configuration template](../../runtime/templates/config.json)
