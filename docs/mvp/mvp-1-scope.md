# MVP 1 Scope

MVP 1 for HadesOS is a macOS-first prosumer and SMB companion focused on safe context awareness, low-risk recommendations, draft actions, approval flows, auditability, and reversible local workflows.

## Included

- File metadata observation and approved reversible file cleanup preparation.
- Calendar context reads and draft calendar changes.
- Slack summaries and message drafts that require human review before sending.
- GitHub issue and pull request context plus draft comments.
- Read-first HomeKit/Matter state observation without device control.
- Safety-kernel action proposals, approval requests, audit events, and rollback metadata.

## Excluded

- Autonomous external sends.
- Privileged system changes.
- Production infrastructure writes.
- Autonomous physical control.
- Camera surveillance, access control, emergency-system integration, or robotics.
- Runtime, connector, cloud, package-manager, or validation-tool implementation in the contracts layer.

## Contract links

The MVP 1 machine-readable contract layer is documented in [`../../packages/contracts/README.md`](../../packages/contracts/README.md). Schemas live in [`../../packages/contracts/schemas/`](../../packages/contracts/schemas/) and examples live in [`../../packages/contracts/examples/`](../../packages/contracts/examples/).
