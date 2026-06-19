# HadesOS

**HadesOS** is a privacy-first ambient AI system app by Luca Dynamics for personal, home, office, startup, and enterprise environments.

HadesOS helps people and teams understand, automate, secure, and control their devices, spaces, systems, and workflows through a calm Apple-level desktop and mobile experience.

> **Tagline:** Calm intelligence for everything around you.

## Product Definition

HadesOS is not a replacement operating system, command center, surveillance product, or autonomous physical-control system. It is a system-level AI application layer that runs across desktop, mobile, smart home, office, and enterprise environments while keeping humans in control.

The product combines:

- Local-first device and context awareness
- Permission-based automations
- Human approval for sensitive actions
- Enterprise-grade auditability
- Privacy-first memory and model routing
- Safe connectors for apps, devices, spaces, and workflows

## Product Layers

### Personal Hades

For normal users managing personal devices, files, apps, calendars, homes, and routines.

### Hades Business

For teams and small companies managing shared tools, office workflows, approvals, onboarding, incidents, and device visibility.

### Hades Enterprise

For organizations needing role-based access, SSO/SCIM, compliance logs, device intelligence, security workflows, model governance, and enterprise integrations.

## Core Architecture

HadesOS is built from scratch around a local-first, cloud-coordinated architecture:

- **Hades Runtime:** local secure runtime for device context, approvals, local inference, encryption, and workflow execution.
- **Cloud Coordinator:** synchronization, organization management, multi-device coordination, and enterprise control plane.
- **Context Engine:** normalized understanding of users, devices, apps, files, spaces, policies, events, and past actions.
- **Agent Orchestrator:** multi-agent planning, verification, and execution behind one simple user experience.
- **Model Router:** policy-aware routing across local models, cloud models, vision, speech, deterministic workflows, and private enterprise models.
- **Safety & Permission Kernel:** deterministic risk classification, approval rules, forbidden-action enforcement, and human override.
- **Memory System:** event log, relational state, knowledge graph, vector retrieval, and encrypted object storage.
- **Connector Framework:** signed least-privilege integrations for operating systems, SaaS tools, smart home systems, identity, security, sensors, and later robotics.
- **Automation Engine:** deterministic execution of approved workflows with previews, rollback metadata, and audit logs.
- **Enterprise Admin Layer:** RBAC/ABAC, SSO, SCIM, policy templates, audit exports, compliance controls, and data residency.

## Initial MVP Direction

The first realistic product should be a macOS-first prosumer and SMB companion that connects devices, files, calendars, Slack, GitHub/Jira, and simple workflows. It should focus on understanding context, drafting actions, recommending safe automations, and executing approved reversible workflows.

High-risk physical control, cameras, access control, emergency-system integration, production infrastructure writes, and robotics should be delayed until the safety, audit, and compliance foundations are mature.

## Core Principles

- Calm and simple user experience
- Privacy-first architecture
- Permission-based automation
- Human approval for sensitive actions
- Local-first where possible
- Enterprise-ready security
- Transparent audit history
- Safe AI execution
- No covert surveillance
- No dangerous autonomous physical actions
- Strong human override


## Repository Structure

`PRODUCT_ARCHITECTURE.md` remains the canonical HadesOS vision document. The repository foundation below is the engineering execution layer that translates that vision into buildable boundaries, contracts, and MVP constraints without adding application implementation yet.

- `apps/` — future user-facing clients.
  - `apps/desktop/` — macOS-first desktop experience.
  - `apps/mobile/` — mobile companion for approvals and glanceable status.
  - `apps/web-admin/` — future organization administration surface.
- `packages/` — future shared local and cross-platform product packages.
  - `packages/runtime/` — local runtime boundary.
  - `packages/context-engine/` — normalized context boundary.
  - `packages/agent-orchestrator/` — planning and verification boundary.
  - `packages/model-router/` — policy-aware model routing boundary.
  - `packages/safety-kernel/` — deterministic safety and approval boundary.
  - `packages/connectors/` — typed connector framework boundary.
  - `packages/automation-engine/` — deterministic workflow execution boundary.
- `services/` — future cloud-coordination service boundaries.
  - `services/api/` — account, organization, policy, and sync APIs.
  - `services/events/` — event ingestion and distribution.
  - `services/ai-gateway/` — governed model access.
- `docs/` — engineering execution documents.
  - `docs/adr/` — architecture decision records.
  - `docs/product/` — product and UX execution specs.
  - `docs/architecture/` — system architecture notes.
  - `docs/security/` — safety, permission, privacy, and audit contracts.
  - `docs/connectors/` — connector contracts and examples.
  - `docs/mvp/` — MVP scope and sequencing boundaries.

## Engineering Execution Docs

- [MVP 1 Scope](docs/mvp/mvp-1-scope.md)
- [Desktop and Mobile UX Spec](docs/product/desktop-mobile-ux-spec.md)
- [Safety Kernel Contract](docs/security/safety-kernel-contract.md)
- [Connector Contract](docs/connectors/connector-contract.md)
- [ADR 0001: Local-First, Cloud-Coordinated Architecture](docs/adr/0001-local-first-cloud-coordinated-architecture.md)
- [ADR 0002: Native-First Desktop and Mobile Strategy](docs/adr/0002-native-first-desktop-and-mobile-strategy.md)
- [ADR 0003: Rust Local Runtime Foundation](docs/adr/0003-rust-local-runtime-foundation.md)
- [ADR 0004: Policy-First Model Router](docs/adr/0004-policy-first-model-router.md)
- [ADR 0005: Deterministic Safety Kernel](docs/adr/0005-deterministic-safety-kernel.md)
- [ADR 0006: Typed Connector Framework](docs/adr/0006-typed-connector-framework.md)

## Detailed Product Architecture

See [`PRODUCT_ARCHITECTURE.md`](PRODUCT_ARCHITECTURE.md) for the full product definition, positioning, user experience, technical architecture, agent system, model router, safety kernel, memory design, connectors, stack recommendations, roadmap, compliance strategy, business strategy, risks, and final architecture verdict.

## Status

Early product architecture phase under Luca Dynamics.
