# HadesOS Contracts

This package contains the first machine-readable contract layer for HadesOS. It translates the safety kernel and connector contract documentation into stable, version-aware JSON Schemas and synthetic examples that future Rust, native, cloud, model-router, connector, and UI implementations can share.

## Contents

- [`schemas/`](schemas/): JSON Schema definitions for action proposals, approval requests, audit events, rollback metadata, and connector manifests.
- [`examples/`](examples/): realistic MVP 1 example JSON documents that validate against the schemas.
- [`fixtures/`](fixtures/): guidance for future deterministic test fixtures.
- [`VALIDATION.md`](VALIDATION.md): validation expectations for future CI without adding tooling yet.

## Contract versioning

Schemas include a `contract_version` field using the `hadesos.contracts.v1` value. Future breaking changes should introduce a new version rather than changing the meaning of existing fields in place.

## Scope

This package is documentation and schema-only. It does not implement the HadesOS runtime, safety kernel, connectors, package management, validation tooling, or CI workflows.
