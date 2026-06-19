# Safety Kernel Contract

The HadesOS safety kernel is the deterministic boundary that classifies risk, checks policy, requests human approval, blocks forbidden actions, records audit events, and preserves rollback metadata for reversible operations.

## Machine-readable schemas

The first versioned contract schemas live in [`../../packages/contracts/schemas/`](../../packages/contracts/schemas/):

- [`action-proposal.schema.json`](../../packages/contracts/schemas/action-proposal.schema.json)
- [`approval-request.schema.json`](../../packages/contracts/schemas/approval-request.schema.json)
- [`audit-event.schema.json`](../../packages/contracts/schemas/audit-event.schema.json)
- [`rollback-metadata.schema.json`](../../packages/contracts/schemas/rollback-metadata.schema.json)

Typed MVP 1 examples live in [`../../packages/contracts/examples/`](../../packages/contracts/examples/), including the file cleanup proposal, approval request, audit event, and rollback metadata examples.

## Shared fields

Safety-kernel payloads use stable identifiers, `contract_version`, `schema_name`, `schema_version`, timestamps, correlation IDs, actor/requester metadata, connector IDs, capabilities, actions, targets, risk class, data classification, policy decision, execution mode where applicable, and rollback references where a reversible action is proposed.

## Risk classes

- `observe`
- `sensitive_read`
- `draft`
- `reversible_write`
- `external_send`
- `privileged_change`
- `physical_control`
- `forbidden`

## Requested by

- `user`
- `automation`
- `agent`
- `system`

## Policy decisions

- `allowed`
- `denied`
- `approval_required`
- `expired`
- `blocked_forbidden`
- `blocked_scope`
- `blocked_policy`

## MVP 1 safety posture

MVP 1 should stay inside observe, sensitive read, draft, and low-risk reversible write workflows. External send, privileged change, physical control, and forbidden actions are not runtime goals for MVP 1.
