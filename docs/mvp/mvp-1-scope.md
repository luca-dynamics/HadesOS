# MVP 1 Scope

## Product goal

MVP 1 proves that HadesOS can be a calm macOS-first personal, prosumer, and SMB companion that understands everyday context, proposes useful actions, asks for approval when needed, and records what happened without becoming a replacement operating console, surveillance product, or autonomous physical-control system.

The MVP should validate the product's core trust loop: connect limited context, explain what HadesOS knows, propose useful next steps, request approval for meaningful effects, execute only bounded reversible work, and produce audit records users can understand.

## Target users

- Founders, creators, operators, and technical prosumers managing files, calendars, apps, and daily workflows.
- Small teams that need lightweight visibility into work context, approvals, and reversible automations.
- Privacy-conscious users who want local-first memory and clear audit history.

## Included features

- macOS-first local runtime shell.
- Home surface with plain-language daily context and useful suggestions.
- Activity timeline for observations, approvals, actions, denials, failures, and rollback events.
- Ask Hades for grounded questions and draft actions within connected context.
- Approval cards that show action, reason, risk, affected systems, rollback plan, and expiration.
- Calendar metadata connector.
- File metadata connector.
- App metadata connector for local application state and basic usage context.
- Optional read-first Slack and GitHub/Jira-style collaboration metadata exploration where scopes are least-privilege.
- HomeKit/Matter read-first exploration for device and room status only, with no physical control.
- Simple reversible automations with dry-run previews, explicit approval, rollback metadata, and audit events.
- Local encrypted memory for user-visible context and audit references.
- Policy-aware model router boundary.
- Safety-kernel boundary for action proposals, approvals, denials, forbidden blocks, audit events, and rollback records.

## Excluded features

- Cameras and visual monitoring.
- Access control systems, locks, badges, or building entry workflows.
- Robotics, drones, vehicles, machinery, or autonomous physical devices.
- Emergency systems, alarms, medical alerts, fire systems, or life-safety workflows.
- Production infrastructure writes, deployments, database mutations, or destructive DevOps actions.
- Employee surveillance, keystroke monitoring, covert productivity scoring, or hidden activity tracking.
- Autonomous security response such as disabling accounts, quarantining devices, or blocking networks.
- High-risk physical control including HVAC, doors, vehicles, industrial systems, or machinery.
- Broad connector marketplace, app store mechanics, or third-party connector distribution.
- Enterprise compliance exports, legal hold, data residency controls, SSO, SCIM, or full admin governance.

## Non-goals

- Replace macOS, iOS, MDM, SIEM, smart home hubs, or project-management tools.
- Build a broad connector marketplace.
- Build enterprise SSO, SCIM, legal hold, data residency, or compliance exports.
- Build fully autonomous agents.
- Optimize for dense admin dashboards or security operations workflows.
- Implement production runtime code for the contracts package before the docs and schemas are validated.
- Add package managers, dependencies, CI workflows, validation scripts, app frameworks, or generated types as part of the documentation reconciliation.

## Success criteria

- A user can understand what HadesOS knows, why it matters, and what it is allowed to do.
- A user can approve, deny, or ignore a proposed reversible action with confidence.
- Every meaningful action produces an audit event with policy, approval, executor, and rollback metadata where applicable.
- MVP connectors are read-heavy, least-privilege, revocable, and fixture-tested.
- Local encrypted memory can be inspected, retained, or deleted by the user.
- The safety kernel blocks forbidden actions and fails closed when policy, authorization, validation, or audit persistence is uncertain.
- The product feels calm, useful, and trustworthy rather than technical or surveillance-oriented.

## First wedge

The first wedge is a macOS personal work companion that summarizes calendar, file, and app context; answers questions about the user's day and workspace; proposes small reversible automations; and asks for explicit approval before execution.

The first wedge should prove the approval and audit experience before expanding into broader team, enterprise, smart-space, or physical-world capabilities.

## What must not be built yet

Do not build physical-control features, surveillance features, autonomous security response, production write actions, enterprise compliance infrastructure, connector marketplace mechanics, broad cross-platform clients, package tooling, generated types, validation scripts, CI workflows, or app frameworks before the MVP 1 safety, audit, memory, and connector contracts are validated.

## Contract links

- Safety-kernel contract: [`../security/safety-kernel-contract.md`](../security/safety-kernel-contract.md)
- Connector contract: [`../connectors/connector-contract.md`](../connectors/connector-contract.md)
- Contracts package: [`../../packages/contracts/README.md`](../../packages/contracts/README.md)
- Schemas: [`../../packages/contracts/schemas/`](../../packages/contracts/schemas/)
- Examples: [`../../packages/contracts/examples/`](../../packages/contracts/examples/)
- Connector manifest schema: [`../../packages/contracts/schemas/connector-manifest.schema.json`](../../packages/contracts/schemas/connector-manifest.schema.json)
- Action proposal schema: [`../../packages/contracts/schemas/action-proposal.schema.json`](../../packages/contracts/schemas/action-proposal.schema.json)
- Approval request schema: [`../../packages/contracts/schemas/approval-request.schema.json`](../../packages/contracts/schemas/approval-request.schema.json)
- Audit event schema: [`../../packages/contracts/schemas/audit-event.schema.json`](../../packages/contracts/schemas/audit-event.schema.json)
- Rollback metadata schema: [`../../packages/contracts/schemas/rollback-metadata.schema.json`](../../packages/contracts/schemas/rollback-metadata.schema.json)
