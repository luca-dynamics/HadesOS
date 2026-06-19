# Connector Contract

HadesOS connectors are signed, least-privilege adapters that expose declared capabilities to the runtime and safety kernel. Connectors must describe their data scopes, action scopes, risk classes, execution modes, data classifications, authorization style, audit events, and test fixture expectations before implementation work begins.

## Machine-readable schema

The connector manifest schema lives at [`../../packages/contracts/schemas/connector-manifest.schema.json`](../../packages/contracts/schemas/connector-manifest.schema.json).

MVP 1 connector examples live in [`../../packages/contracts/examples/`](../../packages/contracts/examples/):

- calendar connector manifest
- file metadata connector manifest
- Slack connector manifest
- GitHub connector manifest
- HomeKit Matter read-first connector manifest

## Execution modes

- `local_only`
- `cloud_only`
- `local_first`
- `cloud_brokered`
- `enterprise_private`

## Data classifications

- `public`
- `personal`
- `confidential`
- `business_sensitive`
- `regulated`
- `physical_environment_sensitive`

## MVP 1 connector posture

MVP 1 connectors should prefer read-first, draft-only, and reversible operations. Smart home examples must remain read-first and must not include autonomous physical control.
