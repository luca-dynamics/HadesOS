# Safety Kernel Contract

The HadesOS safety kernel is the deterministic boundary between AI planning and real-world effects. It classifies risk, checks policy, requests human approval, blocks forbidden actions, records audit events, preserves rollback metadata for reversible operations, and ensures a human can override or stop execution.

The safety kernel is not an agent and does not decide product strategy. It is a constrained policy and execution gate that turns proposed actions into one of: allowed observation, approval request, denial, forbidden block, or audited execution decision.

## Machine-readable schemas and examples

The versioned safety-kernel schemas live in [`../../packages/contracts/schemas/`](../../packages/contracts/schemas/):

- [`action-proposal.schema.json`](../../packages/contracts/schemas/action-proposal.schema.json): proposed action payload submitted to the safety kernel before execution.
- [`approval-request.schema.json`](../../packages/contracts/schemas/approval-request.schema.json): human-readable approval payload derived from a proposal that needs explicit consent.
- [`audit-event.schema.json`](../../packages/contracts/schemas/audit-event.schema.json): durable record of observations, proposals, policy decisions, approvals, denials, executions, failures, and rollback events.
- [`rollback-metadata.schema.json`](../../packages/contracts/schemas/rollback-metadata.schema.json): required rollback description for reversible writes.

Relevant MVP 1 examples live in [`../../packages/contracts/examples/`](../../packages/contracts/examples/):

- [`file-cleanup.action-proposal.example.json`](../../packages/contracts/examples/file-cleanup.action-proposal.example.json)
- [`file-cleanup.approval-request.example.json`](../../packages/contracts/examples/file-cleanup.approval-request.example.json)
- [`file-cleanup.audit-event.example.json`](../../packages/contracts/examples/file-cleanup.audit-event.example.json)
- [`file-cleanup.rollback-metadata.example.json`](../../packages/contracts/examples/file-cleanup.rollback-metadata.example.json)

These contracts are schema-only and do not provide runtime enforcement, validation tooling, or generated types yet.

## Shared contract fields

Safety-kernel payloads use stable identifiers and explicit correlation fields so future runtime, connector, UI, and audit systems can reason about the same event chain. Payloads should include:

- `contract_version` for the versioned HadesOS contract family.
- `schema_name` and `schema_version` for the concrete payload type.
- Stable IDs for proposals, approvals, audit events, rollback metadata, actors, connectors, capabilities, and targets.
- Timestamps for creation, expiration, decision, execution, and rollback events where applicable.
- Correlation IDs that link proposal, approval, execution, audit, and rollback records.
- Requester or actor metadata describing whether the request came from a user, automation, agent, or system process.
- Connector ID, capability name, requested action, target descriptors, risk class, data classification, and policy decision.
- Execution mode and rollback references when a reversible action is proposed.

## Action risk classes

Risk class determines whether an action can proceed, requires approval, or must be blocked.

- `observe`: read low-sensitivity state or metadata already permitted by the user or organization.
- `sensitive_read`: read personal, confidential, business-sensitive, regulated, or physical-environment-sensitive information.
- `draft`: create non-sent, non-applied suggestions such as draft messages, draft calendar events, or proposed file organization plans.
- `reversible_write`: make an approved change that has a clear rollback plan and bounded blast radius.
- `external_send`: send information outside the local user boundary, such as posting a message, emailing a recipient, or commenting in a shared system.
- `privileged_change`: alter permissions, identity, security settings, admin state, production systems, billing, compliance retention, or other high-trust controls.
- `physical_control`: operate or materially affect physical devices, spaces, access, safety systems, vehicles, machinery, locks, cameras, alarms, or environmental controls.
- `forbidden`: action that policy never allows the system to perform.

## Approval requirements

The safety kernel must require explicit human approval when a proposed action crosses a meaningful risk boundary.

- `observe` actions may be allowed when scopes and policy permit them.
- `sensitive_read` actions require clear consent through connector authorization and may require per-action approval when context is unusually sensitive.
- `draft` actions may be generated without execution approval, but must remain visibly non-final and non-sent.
- `reversible_write` actions require approval unless the user has configured a narrow, revocable automation rule with dry-run support and rollback metadata.
- `external_send` actions require explicit approval in MVP 1 and must show recipient, content summary, destination, and expiration.
- `privileged_change` actions are outside MVP 1 runtime scope and must be blocked unless a future policy explicitly enables them.
- `physical_control` actions are outside MVP 1 runtime scope and must be blocked.
- `forbidden` actions must always be blocked and audited.

Approval requests must explain the action, reason, requester, connector, affected target, data classification, risk class, policy decision, expected result, rollback plan when applicable, expiration, and alternatives such as deny or edit.

## Forbidden action registry

The forbidden action registry is the policy list that the safety kernel checks before asking for approval or executing work. MVP 1 forbidden actions include:

- Covert surveillance, hidden tracking, keystroke monitoring, or undisclosed productivity scoring.
- Autonomous physical control of locks, access systems, cameras, alarms, vehicles, robotics, machinery, HVAC, or life-safety systems.
- Emergency response actions, medical alerts, fire systems, or other life-safety workflows.
- Production infrastructure writes, deployments, destructive DevOps actions, database mutations, or irreversible file destruction.
- Identity, access, billing, legal hold, retention, compliance, or security-policy changes.
- Exfiltration of private, confidential, regulated, or business-sensitive data beyond approved scopes.
- Attempts to bypass user approval, connector revocation, organization policy, audit logging, or rollback requirements.

A forbidden block must create an audit event with the proposal reference, policy reason, risk class, requester, affected connector or target, and timestamp.

## Action proposal schema explanation

An action proposal is the input to the safety kernel. It represents what an agent, automation, user action, or system component wants to do before execution.

A proposal should describe:

- Who or what requested the action.
- The connector and capability being used.
- The requested operation and target.
- Why the action is being proposed.
- The risk class and data classification.
- Required scopes and current authorization state.
- Whether the action is a dry run, draft, reversible write, external send, privileged change, or physical-control request.
- Expected user-visible outcome.
- Rollback metadata reference for reversible writes.
- Expiration and correlation metadata for approval and audit records.

The schema is defined in [`action-proposal.schema.json`](../../packages/contracts/schemas/action-proposal.schema.json), with an MVP 1 file-cleanup example in [`file-cleanup.action-proposal.example.json`](../../packages/contracts/examples/file-cleanup.action-proposal.example.json).

## Approval request schema explanation

An approval request is the user-facing decision object produced when policy requires human consent. It should be understandable without reading raw connector payloads.

An approval request should include:

- Proposal and correlation references.
- Plain-language title and summary.
- Requested action, target, connector, requester, and rationale.
- Risk class, data classification, and policy decision.
- Preview or dry-run output when available.
- Rollback summary and rollback metadata reference for reversible writes.
- Approval expiration and available decisions such as approve, deny, or edit.

The schema is defined in [`approval-request.schema.json`](../../packages/contracts/schemas/approval-request.schema.json), with an MVP 1 example in [`file-cleanup.approval-request.example.json`](../../packages/contracts/examples/file-cleanup.approval-request.example.json).

## Audit event schema explanation

An audit event is the durable record of what happened and why. Audit events must be append-friendly, correlation-friendly, and safe to export later for user review or organization compliance.

Audit events should record:

- Event type, timestamp, actor, requester, connector, capability, and target.
- Proposal, approval, execution, denial, failure, or rollback references.
- Policy decision and reason.
- Risk class and data classification.
- Execution result or blocked reason.
- Rollback metadata reference when applicable.
- Redacted summaries instead of unnecessary sensitive payload content.

The schema is defined in [`audit-event.schema.json`](../../packages/contracts/schemas/audit-event.schema.json), with an MVP 1 example in [`file-cleanup.audit-event.example.json`](../../packages/contracts/examples/file-cleanup.audit-event.example.json).

## Rollback metadata requirements

Any `reversible_write` proposal must include rollback metadata before approval. Rollback metadata must describe:

- The original state needed to undo the action.
- The exact target affected by the action.
- The inverse operation or restoration plan.
- Constraints, expiration, or conditions that may make rollback unsafe or impossible.
- The actor authorized to perform rollback.
- User-visible rollback summary.
- Audit linkage between proposal, approval, execution, and rollback events.

If rollback metadata is missing or incomplete, the safety kernel must deny the reversible write or downgrade it to a draft-only proposal.

The schema is defined in [`rollback-metadata.schema.json`](../../packages/contracts/schemas/rollback-metadata.schema.json), with an MVP 1 example in [`file-cleanup.rollback-metadata.example.json`](../../packages/contracts/examples/file-cleanup.rollback-metadata.example.json).

## Human override requirements

HadesOS must preserve human control at every safety boundary.

- Users must be able to deny, cancel, or let approval requests expire.
- Users must be able to revoke connector authorization and stop future actions.
- Users must be able to inspect what was proposed, approved, denied, executed, or rolled back.
- Approved reversible actions must expose rollback when rollback remains safe and available.
- Organization policy may further restrict actions, but must not remove user-visible auditability.
- The system must fail closed when policy, authorization, schema validation, or audit persistence is uncertain.

## MVP 1 safety posture

MVP 1 should stay inside observe, sensitive read, draft, and low-risk reversible write workflows. External send must remain approval-gated. Privileged change, physical control, and forbidden actions are not runtime goals for MVP 1.
