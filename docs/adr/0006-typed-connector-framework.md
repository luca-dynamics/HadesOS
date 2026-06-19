# ADR 0006: Typed Connector Framework

## Status

Accepted for the initial repository foundation.

## Context

HadesOS needs connectors for calendars, files, apps, SaaS tools, smart home systems, identity providers, and future physical systems without creating broad, opaque permissions.

## Decision

Every connector must declare typed capabilities, scopes, data classification, risk classes, execution mode, auth, revocation behavior, dry-run support, audit events, and test fixtures before use.

## Consequences

Connector development becomes slower but safer and easier to review. MVP 1 can start with read-heavy metadata connectors and reversible writes while preserving the path to signed connector governance.

## Alternatives considered

Ad hoc integrations were rejected because they hide risk and make audits unreliable. A marketplace-first connector model was rejected until the internal contract is stable.
