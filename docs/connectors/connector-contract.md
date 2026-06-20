# Connector Contract

HadesOS connectors are signed, least-privilege adapters that expose declared capabilities to the runtime and safety kernel. Connectors translate external systems into typed, revocable, auditable capabilities; they do not grant agents arbitrary API access.

Every connector must be safe to inspect, safe to revoke, testable with synthetic fixtures, and compatible with the safety-kernel proposal, approval, audit, and rollback contracts.

## Machine-readable schema and examples

The connector manifest schema lives at [`../../packages/contracts/schemas/connector-manifest.schema.json`](../../packages/contracts/schemas/connector-manifest.schema.json).

MVP 1 connector examples live in [`../../packages/contracts/examples/`](../../packages/contracts/examples/):

- [`calendar.connector-manifest.example.json`](../../packages/contracts/examples/calendar.connector-manifest.example.json)
- [`file-metadata.connector-manifest.example.json`](../../packages/contracts/examples/file-metadata.connector-manifest.example.json)
- [`slack.connector-manifest.example.json`](../../packages/contracts/examples/slack.connector-manifest.example.json)
- [`github.connector-manifest.example.json`](../../packages/contracts/examples/github.connector-manifest.example.json)
- [`homekit-matter-read-first.connector-manifest.example.json`](../../packages/contracts/examples/homekit-matter-read-first.connector-manifest.example.json)

These contracts are schema-only and do not provide connector runtime code, package managers, validation scripts, generated types, or CI workflows yet.

## Required connector declaration fields

Each connector manifest must declare:

- `contract_version`: versioned HadesOS contract family.
- `schema_name` and `schema_version`: concrete manifest schema identity.
- `connector_id`: stable machine-readable connector identifier.
- `connector_name`: human-readable connector name.
- `domain`: product domain such as scheduling, local files, team communication, software collaboration, or smart spaces.
- `description`: concise explanation of the connector purpose.
- `capabilities`: typed actions the connector exposes.
- `read_scopes`: data the connector may read when authorized.
- `write_scopes`: bounded changes the connector may perform when approved.
- `risk_classes`: risk classes that connector capabilities may produce.
- `data_classification`: sensitivity of data handled by the connector.
- `local_or_cloud_execution_mode`: where execution occurs.
- `auth_method`: authorization mechanism such as OS permission, OAuth, fine-grained token, or platform permission grant.
- `revocation_behavior`: what happens when authorization is revoked.
- `dry_run_support`: whether the connector can preview side effects before execution.
- `audit_events`: event names emitted for reads, drafts, approvals, writes, failures, revocations, and rollbacks.
- `test_fixture_requirements`: synthetic fixture expectations for deterministic future tests.

## Connector execution rules

- Connectors expose typed capabilities, not arbitrary API access.
- Agents, automations, and system components can request connector actions only through action proposals.
- The safety kernel must approve side-effecting actions before an executor calls a connector.
- Connectors must enforce declared scopes and fail closed when authorization is missing or policy is unclear.
- Connectors must degrade safely when auth is revoked, network access fails, data is unavailable, or dry-run preview cannot be produced.
- Connectors must emit or enable audit events for meaningful reads, proposals, approvals, executions, denials, failures, revocations, and rollbacks.
- Connectors must avoid storing unnecessary sensitive payload content and should prefer redacted summaries in audit records.
- Reversible writes must provide rollback metadata before approval.
- MVP 1 connectors must remain read-first, draft-only, or limited to approved reversible operations.

## Execution modes

- `local_only`: connector runs on the user's device and does not require cloud mediation.
- `cloud_only`: connector depends on a cloud API.
- `local_first`: connector prefers local access and may use cloud coordination later.
- `cloud_brokered`: connector uses a HadesOS-managed broker for organization or multi-device coordination.
- `enterprise_private`: connector runs in an organization-controlled environment.

## Data classifications

- `public`
- `personal`
- `confidential`
- `business_sensitive`
- `regulated`
- `physical_environment_sensitive`

## Example: Calendar connector

- `connector_name`: Calendar
- `domain`: scheduling
- `capabilities`: list events, read event metadata, draft event, propose reschedule
- `read_scopes`: event title, time, attendees, location, availability metadata
- `write_scopes`: draft event or reversible event update only after approval
- `risk_classes`: observe, sensitive_read, draft, reversible_write, external_send
- `data_classification`: personal and business-sensitive metadata
- `local_or_cloud_execution_mode`: local first when OS calendar access is available; cloud broker optional later
- `auth_method`: OS permission or OAuth depending on provider
- `revocation_behavior`: stop sync, delete cached tokens, preserve audit records
- `dry_run_support`: required for event creation and changes
- `audit_events`: calendar.read, calendar.draft, calendar.approval_requested, calendar.write, calendar.rollback
- `test_fixture_requirements`: synthetic calendars with personal, team, recurring, and conflict scenarios
- Example manifest: [`calendar.connector-manifest.example.json`](../../packages/contracts/examples/calendar.connector-manifest.example.json)

## Example: File Metadata connector

- `connector_name`: File Metadata
- `domain`: local files
- `capabilities`: index metadata, summarize folders, detect recent changes, draft organization plan
- `read_scopes`: filenames, paths where granted, timestamps, file types, sizes, tags
- `write_scopes`: none for MVP 1 except approved reversible tag or move proposals in later iterations
- `risk_classes`: observe, sensitive_read, draft, reversible_write
- `data_classification`: personal, confidential, and potentially regulated metadata
- `local_or_cloud_execution_mode`: local only for MVP 1
- `auth_method`: OS file permissions and user-selected directories
- `revocation_behavior`: stop indexing revoked paths and purge local cached metadata by policy
- `dry_run_support`: required for any future move, rename, or tag write
- `audit_events`: files.scan, files.indexed, files.proposal, files.write, files.rollback
- `test_fixture_requirements`: synthetic directory trees with nested permissions, aliases, large folders, and sensitive names
- Example manifest: [`file-metadata.connector-manifest.example.json`](../../packages/contracts/examples/file-metadata.connector-manifest.example.json)

## Example: Slack connector

- `connector_name`: Slack
- `domain`: team communication
- `capabilities`: read channel metadata, summarize accessible threads, draft message, send approved message
- `read_scopes`: workspace metadata, channel names, accessible messages, user metadata as granted
- `write_scopes`: post message or reaction only after approval
- `risk_classes`: sensitive_read, draft, external_send
- `data_classification`: business-sensitive communication
- `local_or_cloud_execution_mode`: cloud API connector
- `auth_method`: OAuth with least-privilege scopes
- `revocation_behavior`: revoke token, stop sync, retain audit trail, purge cached content by retention policy
- `dry_run_support`: required for messages and channel changes
- `audit_events`: slack.read, slack.draft, slack.approval_requested, slack.send
- `test_fixture_requirements`: synthetic workspaces, private-channel denial cases, message drafting, and revoked-token tests
- Example manifest: [`slack.connector-manifest.example.json`](../../packages/contracts/examples/slack.connector-manifest.example.json)

## Example: GitHub connector

- `connector_name`: GitHub
- `domain`: software collaboration
- `capabilities`: read repository metadata, summarize issues and pull requests, draft comments, propose labels
- `read_scopes`: repository metadata, issues, pull requests, checks, comments as granted
- `write_scopes`: draft comment or approved non-destructive issue metadata changes only; no production infrastructure writes in MVP 1
- `risk_classes`: observe, sensitive_read, draft, external_send, reversible_write
- `data_classification`: business-sensitive and source-code-adjacent metadata
- `local_or_cloud_execution_mode`: cloud API connector
- `auth_method`: OAuth or fine-grained token
- `revocation_behavior`: revoke token, stop sync, preserve audit, purge cached repository metadata by policy
- `dry_run_support`: required for comments, labels, assignments, and workflow proposals
- `audit_events`: github.read, github.draft, github.approval_requested, github.write
- `test_fixture_requirements`: synthetic repos with issues, pull requests, branch protections, permission-denied cases, and no-op dry runs
- Example manifest: [`github.connector-manifest.example.json`](../../packages/contracts/examples/github.connector-manifest.example.json)

## Example: HomeKit/Matter read-first connector

- `connector_name`: HomeKit/Matter Read-First
- `domain`: smart spaces
- `capabilities`: list rooms, list devices, read device status, summarize offline or unusual state
- `read_scopes`: room names, device names, device type, online status, battery status, non-camera sensor metadata where granted
- `write_scopes`: none in MVP 1
- `risk_classes`: observe, sensitive_read; physical_control is forbidden for MVP 1
- `data_classification`: home and space-sensitive metadata
- `local_or_cloud_execution_mode`: local network or platform-mediated local access
- `auth_method`: OS/home permission grant
- `revocation_behavior`: remove pairing reference, stop polling, purge cached state by policy
- `dry_run_support`: not applicable for read-only MVP 1; required before any future write capability
- `audit_events`: space.read, device.status_read, device.revoked
- `test_fixture_requirements`: synthetic homes with rooms, offline devices, denied devices, and explicitly excluded cameras/locks
- Example manifest: [`homekit-matter-read-first.connector-manifest.example.json`](../../packages/contracts/examples/homekit-matter-read-first.connector-manifest.example.json)

## MVP 1 connector posture

MVP 1 connectors must be read-first, draft-only, or limited to reversible operations with explicit approval, dry-run support, audit events, and rollback metadata. MVP 1 must not include autonomous physical control, covert monitoring, production infrastructure writes, or broad connector marketplace mechanics.
