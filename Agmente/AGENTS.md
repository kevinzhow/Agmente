# Agmente App Layer Guide

## Scope
SwiftUI app layer and protocol routing logic:
- Server management UI
- Session/thread UI state
- ACP vs Codex view model selection

## Architecture Model
- The app has a single coordinator that owns per-server runtime state.
- Each server runtime follows one protocol mode at a time (ACP or Codex).
- Protocol-specific behavior stays isolated behind a shared server view-model contract.
- UI should rely on shared abstractions first, and branch only for protocol-specific screens/controls.

## Architecture Invariants
- `AppViewModel` owns one server view model per server ID.
- ACP and Codex paths must remain protocol-isolated.
- UI should consume unified protocol (`ServerViewModelProtocol`) where possible.
- Session/thread summaries should preserve server metadata (`cwd`, timestamps) when available.

## Change Impact Rules
- Protocol detection changes must validate both first-connect and reconnect behavior.
- Session/thread list parsing changes must preserve ordering and metadata consistency.
- Open-session behavior must not regress summary metadata or current working directory display.
- Add-server form or summary dialog changes must keep ACP and Codex messaging clearly separated.

## Contribution Checklist
- If changing initialization/protocol detection, validate ACP and Codex paths.
- If changing session/thread metadata parsing, verify list + open-session behavior.
- If changing add-server UX, verify both protocol summaries and warnings are accurate.
- If adding capability toggles/settings, persist and restore via existing model/storage patterns.

## Required Tests
- `CodexServerViewModelTests`
- `ViewModelSyncTests`
- `ACPSessionViewModelTests` (when chat/session behavior changes)
- Relevant `AgmenteUITests` coverage (when UI flow or accessibility IDs change)
