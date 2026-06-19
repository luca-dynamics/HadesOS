# Desktop and Mobile UX Spec

HadesOS should feel calm, native, legible, and privacy-preserving. It should not look like a command center, sci-fi dashboard, cyberpunk product, tactical map, or security operations center.

## Desktop

### Home

- Purpose: show what matters now in plain language.
- Primary user: personal users, founders, and SMB operators.
- Main content: daily brief, upcoming calendar context, recent file/app activity, connector health, suggestions, pending approvals.
- Key actions: ask a question, review suggestion, approve safe automation, open Activity, adjust privacy.
- Empty state: invite the user to connect calendar, select folders, and enable local metadata permissions.
- Safety/privacy considerations: show data sources, local-processing status, and why each suggestion appears.

### Spaces

- Purpose: organize homes, offices, rooms, teams, and device groups.
- Primary user: prosumers and SMB operators.
- Main content: spaces list, devices by space, status summaries, shared resources.
- Key actions: add space, rename group, inspect device metadata, review connector permissions.
- Empty state: explain spaces as optional organization, not surveillance zones.
- Safety/privacy considerations: no cameras or access-control actions in MVP 1; read-first device metadata only.

### Devices

- Purpose: provide understandable status for computers, phones, hubs, and approved smart devices.
- Primary user: personal users and SMB operators.
- Main content: device list, health metadata, last seen, connector source, permission state.
- Key actions: view details, revoke connector, troubleshoot stale data.
- Empty state: prompt the user to enable local device discovery or connect supported read-only sources.
- Safety/privacy considerations: avoid covert monitoring, productivity scoring, or high-risk physical control.

### Workflows

- Purpose: manage user-approved routines and reversible automations.
- Primary user: prosumers and SMB operators.
- Main content: drafts, enabled workflows, recent runs, rollback availability, risk labels.
- Key actions: preview, approve, pause, edit, disable, rollback when supported.
- Empty state: offer simple suggestions like calendar preparation or file organization drafts.
- Safety/privacy considerations: all side effects require safety-kernel review and clear audit trails.

### Activity

- Purpose: provide transparent history of observations, decisions, approvals, and outcomes.
- Primary user: all users.
- Main content: timeline, filters, policy decisions, model routing summaries, connector events, rollback events.
- Key actions: inspect event, export later, retry safe action, rollback supported action.
- Empty state: explain that activity will appear as HadesOS observes metadata and proposes actions.
- Safety/privacy considerations: activity must be human-readable and must not expose unnecessary sensitive content.

### Ask Hades

- Purpose: conversational entry point grounded in connected context and permissions.
- Primary user: all users.
- Main content: chat, cited context cards, proposed actions, approval cards, safe alternatives.
- Key actions: ask, refine, create draft, request automation preview, approve or deny proposal.
- Empty state: suggest questions about today, recent files, upcoming meetings, and safe routines.
- Safety/privacy considerations: distinguish answers, drafts, and executable proposals; never imply approval from chat alone.

### Settings

- Purpose: control privacy, connectors, memory, models, notifications, and account settings.
- Primary user: all users; later admins.
- Main content: permissions, local encrypted memory, retention, model preferences, connector revocation, audit controls.
- Key actions: revoke access, delete memory, change routing preference, pause automations.
- Empty state: present defaults and explain recommended privacy posture.
- Safety/privacy considerations: local safety stop and revocation must be easy to find.

## Mobile

### Today

- Purpose: glanceable status and daily context.
- Primary user: personal users and busy operators.
- Main content: short brief, pending approvals, upcoming events, recent safe activity.
- Key actions: approve, snooze, ask, open notification, review source.
- Empty state: invite the user to connect desktop runtime or calendar.
- Safety/privacy considerations: keep sensitive details collapsed by default on lock-screen-like contexts.

### Approvals

- Purpose: review and decide pending actions.
- Primary user: all users.
- Main content: approval cards with action, reason, affected systems, risk, rollback, expiration.
- Key actions: approve, deny, edit when supported, ask why, view audit destination.
- Empty state: reassure the user that HadesOS is waiting for explicit approval before sensitive actions.
- Safety/privacy considerations: no dark patterns; denial is as easy as approval.

### Spaces

- Purpose: quick view of home or office state.
- Primary user: prosumers and SMB operators.
- Main content: spaces, read-only device status, connector health.
- Key actions: inspect space, revoke source, ask about status.
- Empty state: explain optional setup and read-first behavior.
- Safety/privacy considerations: exclude camera feeds, locks, and high-risk physical actions in MVP 1.

### Notifications

- Purpose: calm grouped updates.
- Primary user: all users.
- Main content: approvals, reminders, completed actions, connector issues, policy denials.
- Key actions: open, mute category, change urgency, review source.
- Empty state: explain notification categories and quiet defaults.
- Safety/privacy considerations: avoid alarming language and avoid exposing sensitive content in previews.

### Ask

- Purpose: quick voice/text questions and safe requests.
- Primary user: mobile users away from desktop.
- Main content: concise answers, context cards, draft proposals, links to approvals.
- Key actions: ask, approve linked card, save draft, continue on desktop.
- Empty state: suggest simple questions about schedule, recent activity, or pending approvals.
- Safety/privacy considerations: mobile chat cannot bypass approval or connector scope.

### Settings

- Purpose: mobile control over account, privacy, notifications, connectors, and safety stop.
- Primary user: all users.
- Main content: notification settings, approval preferences, connected desktop, privacy, memory controls.
- Key actions: pause automations, revoke connector, delete synced memory, manage devices.
- Empty state: show recommended defaults and explain what is local versus synced.
- Safety/privacy considerations: emergency pause must be prominent and work even when cloud sync is degraded.
