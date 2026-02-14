# Agmente Unit Tests Guide

## Scope
Unit/integration-style tests for app-layer view models and persistence.

## Test Layers
- Protocol routing and view-model synchronization tests.
- ACP-specific session behavior tests.
- Codex-specific thread/session behavior tests.
- Storage and persistence behavior tests.

## Test Design Rules
- Prefer in-memory storage and deterministic setup.
- Avoid live network dependencies in unit tests.
- Validate protocol-switch behavior explicitly (ACP -> Codex and ACP-only paths).
- Cover metadata behaviors that impact UI ordering and session/thread summaries.
- Keep test names behavior-oriented so refactors do not require doc edits.

## When Updating Tests Is Required
- Any change to session/thread lifecycle logic.
- Any change to protocol detection/switching.
- Any change to summary parsing (`cwd`, timestamps, previews).
