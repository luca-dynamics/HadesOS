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

- [`PRODUCT_ARCHITECTURE.md`](PRODUCT_ARCHITECTURE.md): full product architecture and roadmap.
- [`docs/`](docs/): safety, connector, and MVP scope documentation.
- [`packages/`](packages/README.md): shared package boundaries for future implementations.
- [`packages/contracts/`](packages/contracts/README.md): versioned JSON Schemas and synthetic examples for safety-kernel and connector contracts.

## Detailed Product Architecture

See [`PRODUCT_ARCHITECTURE.md`](PRODUCT_ARCHITECTURE.md) for the full product definition, positioning, user experience, technical architecture, agent system, model router, safety kernel, memory design, connectors, stack recommendations, roadmap, compliance strategy, business strategy, risks, and final architecture verdict.

## Status

Early product architecture phase under Luca Dynamics.
