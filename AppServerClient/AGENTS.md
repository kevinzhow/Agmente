# AppServerClient Package Guide

## Scope
Typed Codex app-server transport/service package used by the iOS app.

## Architecture Model
- Transport and request orchestration are separated from protocol payload parsing.
- Service APIs should remain typed and avoid leaking raw JSON-RPC details to callers.
- Event parsing should map wire notifications/requests into stable app-facing event types.

## Protocol Notes
- Default wire mode omits `"jsonrpc":"2.0"` header, with optional inclusion toggle.
- Handle both notifications and server-initiated requests (for approvals and similar flows).
- Keep event parser mappings aligned with upstream app-server method names.
- Treat method-name and payload-shape drift as compatibility-sensitive changes.

## Extension Pattern
When adding app-server method support:
1. Add method name constant.
2. Add payload model and params encoder.
3. Add typed service wrapper.
4. Add response parser coverage if result is typed.
5. Add or update event parser mapping if notifications/requests are involved.
6. Add package tests for request flow, parse flow, and error handling.

## Tests
- Run package tests for `AppServerClient`.
