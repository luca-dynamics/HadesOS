# MVP 1 Scope

## Product goal

MVP 1 proves that HadesOS can be a calm macOS-first personal, prosumer, and SMB companion that understands everyday context, proposes useful actions, asks for approval when needed, and records what happened without becoming a command center or autonomous control system.

## Target users

- Founders, creators, operators, and technical prosumers managing files, calendars, apps, and daily workflows.
- Small teams that need lightweight visibility into work context, approvals, and reversible automations.
- Privacy-conscious users who want local-first memory and clear audit history.

## Included features

- macOS-first local runtime shell.
- Home surface with plain-language daily context and useful suggestions.
- Activity timeline for observations, approvals, actions, denials, and rollback events.
- Ask Hades for grounded questions and draft actions within connected context.
- Approval cards that show action, reason, risk, affected systems, rollback plan, and expiration.
- Calendar metadata connector.
- File metadata connector.
- App metadata connector for local application state and basic usage context.
- Simple reversible automations with dry-run previews.
- Local encrypted memory for user-visible context and audit references.
- Policy-aware model router boundary.
- Audit trail for model routing, safety decisions, approvals, execution, and rollback.

## Excluded features

- Cameras and visual monitoring.
- Access control systems, locks, badges, or building entry workflows.
- Robotics, drones, or autonomous physical devices.
- Emergency systems, alarms, medical alerts, fire systems, or life-safety workflows.
- Production infrastructure writes, deployments, database mutations, or destructive DevOps actions.
- Employee surveillance, keystroke monitoring, covert productivity scoring, or hidden activity tracking.
- Autonomous security response such as disabling accounts, quarantining devices, or blocking networks.
- High-risk physical control including HVAC, doors, vehicles, industrial systems, or machinery.

## Non-goals

- Replace macOS, iOS, MDM, SIEM, smart home hubs, or project-management tools.
- Build a broad connector marketplace.
- Build enterprise SSO, SCIM, legal hold, data residency, or compliance exports.
- Build fully autonomous agents.
- Optimize for dense admin dashboards or security operations workflows.

## Success criteria

- A user can understand what HadesOS knows, why it matters, and what it is allowed to do.
- A user can approve or deny a proposed reversible action with confidence.
- Every meaningful action produces an audit event with policy, approval, executor, and rollback metadata.
- MVP connectors are read-heavy, least-privilege, revocable, and fixture-tested.
- Local encrypted memory can be inspected, retained, or deleted by the user.
- The product feels calm, useful, and trustworthy rather than technical or surveillance-oriented.

## First wedge

The first wedge is a macOS personal work companion that summarizes calendar, file, and app context; answers questions about the user's day and workspace; proposes small reversible automations; and asks for explicit approval before execution.

## What must not be built yet

Do not build physical-control features, surveillance features, autonomous security response, production write actions, enterprise compliance infrastructure, connector marketplace mechanics, or broad cross-platform clients before the MVP 1 safety, audit, memory, and connector contracts are validated.
