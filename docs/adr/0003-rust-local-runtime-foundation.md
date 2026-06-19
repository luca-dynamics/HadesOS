# ADR 0003: Rust Local Runtime Foundation

## Status

Accepted for the initial repository foundation.

## Context

The local runtime will eventually handle encrypted memory, deterministic execution, connector adapters, policy checks, and potentially long-running background tasks.

## Decision

Use Rust as the intended foundation for the local runtime once implementation begins. Keep this repository PR documentation-only and avoid adding toolchains or crates yet.

## Consequences

Rust gives strong memory safety, predictable binaries, and good boundaries for typed executors. The team must still design ergonomic FFI/API seams for native apps and avoid premature framework coupling.

## Alternatives considered

Swift-only was rejected because HadesOS is intended to span platforms. TypeScript-only was rejected for the privileged local runtime because deterministic executors and local security boundaries benefit from a systems language.
