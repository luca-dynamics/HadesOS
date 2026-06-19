# HadesOS Product Architecture

## 1. Product Definition

HadesOS is a calm, permission-based ambient AI system layer by Luca Dynamics for personal devices, homes, offices, startups, and enterprise environments. It is not a replacement operating system, command center, military system, or surveillance product. It is a premium system app that helps people understand, automate, secure, and coordinate their digital and physical environments while keeping humans in control.

HadesOS solves the gap between isolated AI assistants, fragmented smart home apps, automation tools, security dashboards, and enterprise management consoles. A normal user should be able to ask why a device is behaving strangely, create a safe home routine, summarize activity across apps, or approve a suggested automation. A company should be able to understand device posture, coordinate workflows, enforce policy, and review auditable AI-assisted actions without giving an autonomous agent unsafe power.

Primary audiences:

- Consumers and families who want simple device, home, file, calendar, and safety awareness.
- Prosumer operators, founders, creators, and technical households that want reliable automation without brittle scripting.
- Small businesses that need office visibility, onboarding/offboarding workflows, and app/device coordination.
- Enterprises that need policy-aware AI operations across identity, devices, SaaS tools, logs, facilities, and eventually robotics.

HadesOS differs from adjacent categories because it is cross-domain and safety-governed:

- Unlike a normal AI assistant, it has persistent context, device integrations, policy checks, approval flows, and audited execution.
- Unlike a smart home app, it spans files, apps, identity, devices, enterprise SaaS, and workplace operations.
- Unlike MDM, it is user-facing and workflow-aware rather than only device-policy-focused.
- Unlike security tools, it emphasizes explainability, prevention, and safe response instead of only alerts.
- Unlike automation apps, it has a planning, verification, permission, and audit layer around every meaningful action.

## 2. Product Positioning

One-line description: HadesOS is a privacy-first ambient AI layer that helps people and teams understand, automate, and secure the devices, spaces, apps, and workflows around them.

Consumer positioning: a beautiful personal system companion for your devices, home, files, routines, and everyday digital life.

Business positioning: an AI operations layer for small teams that connects apps, devices, office workflows, approvals, and security basics.

Enterprise positioning: a governed AI orchestration and context layer for identity-aware automation, device intelligence, operational workflows, incident response, and compliance-grade auditability.

Recommended tagline: **Calm intelligence for everything around you.**

## 3. User Experience and Interface

The product should feel closer to Apple Home, Find My, Shortcuts, Screen Time, and System Settings than to a sci-fi dashboard. The interface should be quiet, spatial, human, and confidence-building. It should avoid red-alert aesthetics, tactical maps, dense telemetry grids, or command-center metaphors.

### Desktop app

Primary desktop surfaces:

1. **Home**: a plain-language summary of what matters now: devices, spaces, workflows, upcoming events, suggested automations, and security posture.
2. **Spaces**: rooms, offices, locations, device groups, sensors, access points, and shared resources.
3. **Devices**: computers, phones, tablets, smart home hubs, printers, cameras, network devices, and managed endpoints.
4. **Workflows**: automations, approvals, recurring tasks, onboarding/offboarding, routines, and incident playbooks.
5. **Activity**: a human-readable timeline of observations, recommendations, approvals, actions, and outcomes.
6. **Ask Hades**: conversational interface grounded in connected context and bounded by permissions.
7. **Settings**: integrations, privacy, retention, permissions, local processing, model preferences, and account controls.

Normal users should first see a calm Home screen with a short daily brief, device health, privacy status, and two or three useful suggestions. Enterprise admins should first see organization posture, policy exceptions, pending approvals, integration health, and recent high-confidence incidents.

### Mobile app

Mobile should focus on glanceable status and approvals:

- Today: brief status, routines, pending approvals, recent activity.
- Approvals: simple cards showing requested action, reason, risk, affected systems, alternatives, and expiration.
- Spaces: home or office state with device and sensor summaries.
- Notifications: grouped, calm, and severity-labeled.
- Ask: voice/text interaction for safe queries and approved actions.

### Interaction tone

Notifications should be specific and non-alarmist. Instead of “Threat detected,” say “Unusual sign-in pattern noticed for Notion. Review before Hades takes action.” Approval cards should expose: action, target, why now, confidence, risk class, rollback plan, audit destination, and who requested it.

## 4. Core Architecture

HadesOS should be built as a local-first, cloud-coordinated system.

### Local runtime

The local runtime runs on macOS, Windows, iOS, Android, and eventually edge gateways. It handles local context collection, local model inference where possible, encryption, device control adapters, offline automations, and user approvals. It should never require cloud access for basic local visibility or emergency user override.

### Cloud coordinator

The cloud coordinator synchronizes encrypted metadata, routes enterprise workflows, manages organizations, coordinates multi-device state, runs high-scale jobs, hosts admin services, and brokers connectors that cannot run locally.

### Context engine

The context engine normalizes devices, users, spaces, files, SaaS objects, policies, sensor events, and historical actions into a shared representation. It should maintain source provenance and confidence for every fact.

### Agent orchestrator

The orchestrator decomposes user requests or events into plans, calls specialized agents, asks the safety kernel for authorization, verifies preconditions, executes approved steps, and records outcomes.

### Model router

The model router selects local models, cloud models, vision models, speech models, deterministic workflows, and enterprise-hosted private models based on privacy, latency, cost, accuracy, risk, data classification, and policy.

### Memory system

Memory should combine an append-only event log, relational state store, knowledge graph, vector index, and secure object store. Sensitive memories must have retention controls, user visibility, deletion support, tenant isolation, and cryptographic protection.

### Safety and permission kernel

The safety kernel classifies action risk, checks user and enterprise policy, enforces approvals, blocks forbidden actions, and requires rollback plans for reversible high-impact operations.

### Audit layer

The audit layer records observations, plans, model/tool calls, policy decisions, approvals, denials, execution results, and rollback events. Enterprise logs should support export to SIEM, immutable storage, legal hold, and retention policies.

### Connector framework

Connectors are signed, least-privilege adapters for OS APIs, SaaS APIs, smart home protocols, identity providers, security tools, sensors, and later robotics. Every connector must declare capabilities, data scopes, action scopes, risk classes, and test fixtures.

### Automation engine

The automation engine executes deterministic workflows, scheduled routines, event triggers, and agent-proposed playbooks. The safest architecture is AI-planned but deterministic-executed: the AI suggests or composes plans, while typed actions execute through constrained APIs.

### Enterprise admin layer

The admin layer provides RBAC, ABAC, SSO, SCIM, policy templates, device groups, connector governance, approval chains, audit exports, model controls, data residency, and compliance reporting.

## 5. AI Agent System

HadesOS should use a multi-agent internal architecture behind a single simple user experience. Users should not manage agents. They should experience one coherent product.

Recommended internal agents:

- **Concierge Agent**: user-facing conversation and explanation.
- **Context Agent**: retrieves relevant facts and checks provenance.
- **Planner Agent**: decomposes goals into proposed steps.
- **Verifier Agent**: checks feasibility, preconditions, conflicts, and risk.
- **Safety Agent**: interfaces with the deterministic safety kernel but does not override it.
- **Automation Agent**: translates approved plans into typed workflows.
- **Security Agent**: detects suspicious events and recommends responses.
- **Admin Agent**: supports enterprise policy and governance tasks.
- **Connector Agents**: domain-specific adapters for SaaS, devices, smart home, and sensors.

Coordination should follow plan-review-execute:

1. Gather context with citations/provenance.
2. Generate a bounded plan.
3. Classify risk.
4. Verify preconditions and permissions.
5. Ask for approval when needed.
6. Execute through typed tools only.
7. Confirm outcome independently.
8. Write audit record and rollback metadata.

To avoid hallucinated or unsafe actions, agents must not directly call arbitrary system APIs. They should operate through schemas, allowlists, capability tokens, deterministic validators, dry-run previews, source-grounded retrieval, and policy gates.

## 6. Model Router

The model router should be policy-first, not benchmark-first. It should evaluate every task against data sensitivity, action risk, latency, cost, accuracy requirement, modality, user preference, tenant policy, and availability.

Routing policy examples:

- Local small model: private summarization, classification, simple automation suggestions, offline Q&A over local metadata.
- Local vision model: on-device camera/screen interpretation when privacy-sensitive.
- Cloud frontier model: complex planning, deep reasoning, long-context synthesis, and advanced coding/workflow generation after redaction and policy approval.
- Speech model: local wake/command detection where possible; cloud transcription only with consent and retention controls.
- Deterministic workflow: anything compliance-critical, repetitive, or high-risk.
- Enterprise private model: regulated data, contractual data-boundary requirements, sensitive corporate knowledge, or customer-selected deployments.

State-of-the-art architecture:

- Policy engine before inference.
- Data classification and redaction layer.
- Model capability registry.
- Cost/latency/quality scoring.
- Risk-aware fallback plans.
- Evaluation harness with golden tasks.
- Per-tenant model allowlists.
- Full inference audit metadata without storing unnecessary raw prompts.

## 7. Safety and Permission Kernel

Risk classes:

- **Low risk**: read-only summaries, device status, calendar explanations, draft suggestions, local reminders.
- **Medium risk**: reversible automations, sending non-sensitive notifications, changing non-critical preferences, creating drafts, moving files to a recoverable location.
- **High risk**: account changes, deleting data, changing permissions, sending external messages, modifying security settings, unlocking doors, disabling cameras, spending money, production changes.
- **Critical**: actions affecting physical safety, emergency systems, access control, financial transfers, legal/compliance posture, employee termination, production infrastructure, robotics movement near people.
- **Forbidden**: harming people, trapping people, disabling emergency services, bypassing safety interlocks, covert surveillance, credential theft, destructive actions without recovery, evading law enforcement, weapons-related operation, impersonation, or policy bypass.

Approval rules:

- Low risk: may execute automatically if user has enabled the relevant capability.
- Medium risk: execute automatically only with prior user-configured rules and visible audit trail; otherwise ask.
- High risk: explicit just-in-time user approval with preview and rollback plan.
- Critical: multi-party approval, enterprise policy check, time delay when appropriate, and emergency exception handling.
- Forbidden: never execute, even with approval.

Emergency handling should prioritize human safety and legal emergency systems. HadesOS may notify, illuminate, unlock according to existing life-safety policy, call approved emergency contacts, or provide instructions, but it must not block exits, disable alarms, conceal incidents, or override emergency responders.

Human override must be physical and obvious: local kill switch in apps, hardware-level stop for robotics later, admin disable switch, connector revoke, offline safe mode, and visible “Hades is paused” state.

## 8. Memory and Context Engine

HadesOS should represent the world with multiple storage primitives:

- Append-only event log for every observation and action.
- Relational database for users, devices, policies, tenants, workflows, and permissions.
- Knowledge graph for relationships among people, devices, spaces, files, apps, teams, and policies.
- Vector database for semantic retrieval across documents, notes, tickets, logs, and past actions.
- Object store for encrypted artifacts such as screenshots, exported logs, and workflow bundles.

Every memory item needs owner, source, timestamp, confidence, classification, retention policy, consent basis, access scope, and deletion behavior. Consumer memory should default to local storage with opt-in sync. Enterprise memory should default to tenant isolation, administrative policy, and explicit retention controls.

## 9. Connectors and Integrations

First integrations should maximize utility without creating dangerous physical control risk.

MVP connector priorities:

- macOS and Windows device inventory, notifications, files metadata, calendar, and app activity with permissions.
- iOS and Android companion status, approvals, notifications, and limited device context.
- Google Calendar, Gmail metadata, Microsoft 365, Outlook, Slack, Notion, GitHub, Jira, Linear, and Google Drive/OneDrive.
- HomeKit and Matter read-first device state, then limited reversible controls.
- SSO via Google and Microsoft accounts for early business use.

Business and enterprise expansion:

- Okta, Entra ID, Google Workspace admin, SCIM, Jamf, Intune, Kandji, CrowdStrike, SentinelOne, Wiz, Datadog, Splunk, Elastic, ServiceNow, PagerDuty, and SIEM export.
- Cameras and sensors should start with event metadata, not general surveillance. Video analysis should be explicit, local-first when possible, and privacy-zoned.
- Access control and robotics should be delayed until the safety kernel and audit program are mature.

## 10. Technical Stack

Recommended stack:

- **Desktop**: Swift/SwiftUI for macOS first, Kotlin/Compose or native Windows App SDK for Windows later. Avoid Electron for the premium system-app experience and battery footprint. Consider Tauri only for internal admin utilities, not the flagship app.
- **Mobile**: Swift/SwiftUI for iOS and Kotlin/Jetpack Compose for Android. React Native or Flutter can accelerate development, but native is better for permissions, background behavior, privacy affordances, and Apple-level polish.
- **Local runtime**: Rust core for cross-platform safety, performance, secure storage, policy evaluation, connector sandboxing, and deterministic workflow execution.
- **Backend**: Go or Rust for control plane, TypeScript for web/admin surfaces, Python for AI experimentation and evaluation services.
- **AI services**: Python/FastAPI or Ray for evaluation and model experimentation; Rust/Go gateways for production routing.
- **Model serving**: llama.cpp/MLX/Core ML/ONNX Runtime locally; vLLM/Triton for private deployments; managed frontier models through policy-controlled gateways.
- **Event streaming**: Redpanda or Kafka for enterprise-scale events; NATS for lightweight internal messaging and edge deployments.
- **Databases**: Postgres for core state, pgvector or dedicated vector DB for retrieval, Neo4j or TypeDB for graph where graph complexity justifies it, object storage for encrypted artifacts.
- **Security**: OPA/Rego or Cedar for policy, SPIFFE/SPIRE for service identity, KMS/HSM-backed encryption, hardware keystore on devices, signed connectors, and SLSA-oriented build pipelines.
- **Deployment**: Kubernetes for cloud services, Terraform for infrastructure, GitHub Actions or Buildkite for CI/CD, OpenTelemetry for observability.

## 11. MVP Roadmap

### MVP 1: Personal and prosumer desktop companion

Build a macOS-first product with local runtime, Home screen, Activity timeline, Ask Hades, approval cards, calendar/file/app metadata connectors, simple automations, local encrypted memory, model router, and audit log. The wedge should be: “Hades understands your devices, files, calendar, and workflows, then safely drafts and automates routine actions with approval.”

Delay cameras, access control, robotics, production infrastructure writes, autonomous security response, employee surveillance, and high-risk physical controls.

### Phase 2: Small team workspace

Add shared spaces, team workflows, Slack/Google Workspace/Microsoft 365/GitHub/Jira integrations, organization policies, role-based approvals, and admin activity review.

### Phase 3: Enterprise governance

Add SSO, SCIM, RBAC/ABAC, MDM integrations, SIEM export, immutable audit logs, data residency, private model routing, compliance reporting, and advanced policy packs.

### Phase 4: Safe physical environment layer

Add Matter/HomeKit controls, office sensors, badge/access metadata, camera event summaries, and facilities workflows with strict approvals and privacy zones.

### Phase 5: Robotics and embodied systems

Only after safety certification, simulation, physical interlocks, emergency stop, bounded environments, and external safety review should robotics be supported.

## 12. Security, Privacy, and Compliance

Security principles:

- Least privilege connector scopes.
- Local-first processing for sensitive data.
- Tenant isolation and encryption everywhere.
- Explicit consent for data categories.
- No covert monitoring.
- Immutable audit for administrative and high-risk actions.
- Human-readable permissions.
- Revocation that works immediately.

Audit logs should capture who/what requested an action, context used, model/tool selected, policy decision, approval identity, execution status, external API response metadata, and rollback outcome. Logs should be tamper-evident, exportable, and retention-controlled.

SOC 2 and ISO 27001 readiness should start from day one: asset inventory, access reviews, change management, incident response plan, vendor risk management, secure SDLC, vulnerability management, logging, monitoring, backups, disaster recovery, and documented policies.

## 13. Business and Market Strategy

Best early users are technical founders, executive operators, AI-forward teams, security-conscious prosumers, and small companies with too many tools and not enough operations staff.

Do not start broad consumer or heavy enterprise first. Start prosumer/SMB because users have urgent workflow pain, can tolerate a young product, and will pay for cross-app automation with safety and memory.

Investor wedge: a governed AI action layer that begins as a premium productivity/security companion and expands into enterprise AI operations. The valuable moat is not the chat interface; it is the permissioned context graph, connector ecosystem, policy engine, audit trail, and trusted execution layer.

Pricing:

- Free or low-cost personal tier with local-only basics.
- Pro at $15-$30/user/month for advanced connectors, memory, and automations.
- Team at $30-$60/user/month for shared workflows, approvals, and admin.
- Enterprise custom pricing for SSO, SCIM, SIEM, MDM, private models, compliance, and data residency.

## 14. Critical Risks

Engineering risks:

- Connector brittleness across APIs and OS permission models.
- Local runtime complexity across platforms.
- Context quality and entity resolution errors.
- Model hallucination during planning.
- Audit and permission systems becoming afterthoughts.

Mitigation: start with few connectors, typed schemas, deterministic execution, test harnesses, local-first architecture, and safety kernel from the beginning.

Safety risks:

- Over-automation of sensitive actions.
- Privacy violations through excessive context collection.
- Misuse by employers for surveillance.
- Unsafe physical controls.

Mitigation: read-first MVP, explicit consent, privacy zones, forbidden-action list, approval chains, immutable audit, and delayed physical controls.

Product risks:

- Too broad to explain.
- Looks like a scary command center.
- Users do not trust it enough to connect accounts.
- The assistant feels generic.

Mitigation: choose one wedge, design calm interfaces, show exact permissions, explain value before asking for access, and make every action previewable.

Go-to-market risks:

- Consumer market has high support burden and low willingness to pay.
- Enterprise sales cycles are too long for a young product.
- Smart home is fragmented and low-margin.

Mitigation: start with prosumer/SMB operators, sell workflow relief plus safe automation, then move into enterprise governance.

## 15. Final Verdict

HadesOS is a strong product idea if it is treated as a governed ambient AI operations layer, not as an all-powerful autonomous system. The realistic first product is a macOS-first prosumer and SMB companion that connects calendar, files, Slack, GitHub/Jira, device state, and approval-based automations.

The too-ambitious version is a universal environment controller with cameras, access control, emergency systems, and robotics from day one. That version is dangerous, legally complex, expensive, and likely to destroy trust before the product matures.

The best first product is: **a calm AI system app that understands your work context, devices, and routines, then safely drafts, recommends, and executes approved automations with a visible audit trail.**

If founding this company, I would choose:

- macOS + iOS first for premium UX and trust.
- Rust local runtime shared across platforms.
- Postgres/event-log memory foundation.
- Policy-first model router.
- Deterministic automation engine.
- Multi-agent orchestration hidden behind one user experience.
- Strict safety kernel and audit layer in v1, not later.
- Prosumer/SMB wedge before enterprise expansion.
