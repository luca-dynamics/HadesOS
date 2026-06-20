# HadesOS Contracts

This package contains the first machine-readable contract layer for HadesOS. It translates the safety-kernel and connector documentation into stable, version-aware JSON Schemas and synthetic examples that future runtime, native, cloud, model-router, connector, UI, and audit implementations can share.

## Contents

- [`schemas/`](schemas/): JSON Schema definitions for action proposals, approval requests, audit events, rollback metadata, and connector manifests.
- [`examples/`](examples/): synthetic MVP 1 example JSON documents for safety-kernel flows and connector manifests.
- [`fixtures/`](fixtures/): guidance for future deterministic test fixtures.
- [`VALIDATION.md`](VALIDATION.md): validation expectations for future CI without adding tooling yet.

## Schemas

- [`schemas/action-proposal.schema.json`](schemas/action-proposal.schema.json)
- [`schemas/approval-request.schema.json`](schemas/approval-request.schema.json)
- [`schemas/audit-event.schema.json`](schemas/audit-event.schema.json)
- [`schemas/rollback-metadata.schema.json`](schemas/rollback-metadata.schema.json)
- [`schemas/connector-manifest.schema.json`](schemas/connector-manifest.schema.json)

## Examples

- [`examples/file-cleanup.action-proposal.example.json`](examples/file-cleanup.action-proposal.example.json)
- [`examples/file-cleanup.approval-request.example.json`](examples/file-cleanup.approval-request.example.json)
- [`examples/file-cleanup.audit-event.example.json`](examples/file-cleanup.audit-event.example.json)
- [`examples/file-cleanup.rollback-metadata.example.json`](examples/file-cleanup.rollback-metadata.example.json)
- [`examples/calendar.connector-manifest.example.json`](examples/calendar.connector-manifest.example.json)
- [`examples/file-metadata.connector-manifest.example.json`](examples/file-metadata.connector-manifest.example.json)
- [`examples/slack.connector-manifest.example.json`](examples/slack.connector-manifest.example.json)
- [`examples/github.connector-manifest.example.json`](examples/github.connector-manifest.example.json)
- [`examples/homekit-matter-read-first.connector-manifest.example.json`](examples/homekit-matter-read-first.connector-manifest.example.json)

## Canonical narrative docs

- Safety-kernel narrative contract: [`../../docs/security/safety-kernel-contract.md`](../../docs/security/safety-kernel-contract.md)
- Connector narrative contract: [`../../docs/connectors/connector-contract.md`](../../docs/connectors/connector-contract.md)
- MVP 1 scope: [`../../docs/mvp/mvp-1-scope.md`](../../docs/mvp/mvp-1-scope.md)

## Contract versioning

Schemas include a `contract_version` field using the `hadesos.contracts.v1` value. Future breaking changes should introduce a new version rather than changing the meaning of existing fields in place.

## Scope

This package is documentation and schema-only. It does not implement the HadesOS runtime, safety kernel, connectors, package management, validation tooling, generated types, CI workflows, app frameworks, or production execution code.
