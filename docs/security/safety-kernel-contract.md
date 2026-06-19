# Safety Kernel Contract

The safety kernel is the deterministic authority for whether a HadesOS action may be executed. AI agents may propose actions, explain tradeoffs, and prepare drafts, but only typed deterministic executors may perform side effects after safety checks pass.

## Action risk classes

- `observe`: read-only metadata or status with low sensitivity.
- `sensitive_read`: reads personal, confidential, regulated, or business-sensitive data.
- `draft`: creates non-sent, non-executed content or workflow previews.
- `reversible_write`: changes state that can be rolled back with known metadata.
- `external_send`: sends messages, invitations, comments, files, or notifications to others.
- `privileged_change`: changes permissions, identity, billing, security, policy, or shared resources.
- `physical_control`: affects devices or environments in the physical world.
- `forbidden`: blocked regardless of approval until a future ADR explicitly changes policy.

## Approval requirements

- `observe`: allowed when connector scope and user policy permit.
- `sensitive_read`: requires explicit grant, visible reason, and audit event.
- `draft`: allowed with provenance and no side effect.
- `reversible_write`: requires approval unless covered by a user-created automation rule with rollback metadata.
- `external_send`: requires approval showing recipient, content summary, source context, and expiration.
- `privileged_change`: requires explicit approval and may require a second approver in team contexts.
- `physical_control`: forbidden for MVP 1 except read-first device metadata.
- `forbidden`: never executed.

## Forbidden action registry

MVP 1 must register these as forbidden:

- Camera monitoring or visual surveillance.
- Door locks, access control, badges, or entry systems.
- Robotics, vehicles, drones, machinery, and high-risk physical systems.
- Emergency, medical, fire, alarm, or life-safety systems.
- Production infrastructure writes or destructive DevOps actions.
- Employee surveillance, covert monitoring, keystroke logging, or productivity scoring.
- Autonomous security response that disables accounts, blocks access, quarantines devices, or changes network controls.

## Action proposal schema

Required fields:

- `proposal_id`
- `requested_by` (`user`, `automation`, `agent`, or `system`)
- `agent_trace_id` when proposed by an AI agent
- `connector_id`
- `capability`
- `risk_class`
- `target_refs`
- `input_summary`
- `data_classification`
- `reason`
- `preconditions`
- `dry_run_available`
- `rollback_plan_ref` when applicable
- `expires_at`

## Approval request schema

Required fields:

- `approval_id`
- `proposal_id`
- `title`
- `plain_language_summary`
- `risk_class`
- `affected_systems`
- `affected_people_or_spaces`
- `requested_action`
- `why_now`
- `alternatives`
- `rollback_summary`
- `audit_destination`
- `expires_at`
- `approver_requirements`

## Audit event schema

Required fields:

- `event_id`
- `timestamp`
- `actor`
- `event_type`
- `proposal_id`
- `approval_id` when applicable
- `connector_id`
- `executor_id`
- `risk_class`
- `policy_decision`
- `decision_reason`
- `input_hash`
- `output_summary`
- `rollback_ref` when applicable
- `tenant_or_user_scope`
- `retention_policy`

## Rollback metadata requirements

Reversible writes must include:

- prior state reference or compensating action;
- target identifiers;
- executor version;
- time window for safe rollback;
- user-visible rollback summary;
- known rollback limitations;
- audit event linkage.

## Human override requirements

- Users must be able to deny, cancel, or pause pending actions.
- Local emergency stop must not depend on cloud availability.
- Approval cards must never hide material risk behind AI confidence language.
- Denials and overrides must be audited without penalizing the user.
- Team policies may require escalation, but cannot remove a user's local safety stop for their own device.
