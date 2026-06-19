# Connector Contract

Every HadesOS connector must be least-privilege, typed, revocable, testable, and auditable before it can be used by agents or automations.

## Required declaration

Each connector must declare:

- `connector_name`
- `domain`
- `capabilities`
- `read_scopes`
- `write_scopes`
- `risk_classes`
- `data_classification`
- `local_or_cloud_execution_mode`
- `auth_method`
- `revocation_behavior`
- `dry_run_support`
- `audit_events`
- `test_fixture_requirements`

## Execution rules

- Connectors expose typed capabilities, not arbitrary API access.
- Agents can request connector actions only through action proposals.
- The safety kernel must approve side-effecting actions before an executor calls a connector.
- Connectors must degrade safely when auth is revoked or network access fails.
- MVP connectors should prefer read-only metadata and reversible actions.

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

## Example: File metadata connector

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
