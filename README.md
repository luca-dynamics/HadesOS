# HadesOS

**HadesOS** is a privacy-first ambient AI system app by Luca Dynamics for personal, home, office, startup, and enterprise environments.

HadesOS helps people and teams understand, automate, secure, and control their devices, spaces, systems, and workflows through a calm desktop and mobile experience.

> **Tagline:** Calm intelligence for everything around you.

## Canonical vision

The canonical product vision, architecture, roadmap, and positioning live in [`PRODUCT_ARCHITECTURE.md`](PRODUCT_ARCHITECTURE.md). Treat that file as the source of truth for the long-term HadesOS product definition.

## Product definition

HadesOS is not a replacement operating system, surveillance product, or autonomous physical-control system. It is a system-level AI application layer that runs across desktop, mobile, smart home, office, and enterprise environments while keeping humans in control.

The product combines:

- Local-first device and context awareness
- Permission-based automations
- Human approval for sensitive actions
- Enterprise-grade auditability
- Privacy-first memory and model routing
- Safe connectors for apps, devices, spaces, and workflows

## Product layers

### Personal Hades

For people managing personal devices, files, apps, calendars, homes, and routines.

### Hades Business

For teams and small companies managing shared tools, office workflows, approvals, onboarding, incidents, and device visibility.

### Hades Enterprise

For organizations needing role-based access, SSO/SCIM, compliance logs, device intelligence, security workflows, model governance, and enterprise integrations.

## Core architecture

HadesOS is built around a local-first, cloud-coordinated architecture:

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

## Initial MVP direction

The first realistic product should be a macOS-first prosumer and SMB companion that connects devices, files, calendars, Slack, GitHub/Jira, and simple workflows. It should focus on understanding context, drafting actions, recommending safe automations, and executing approved reversible workflows.

High-risk physical control, cameras, access control, emergency-system integration, production infrastructure writes, and robotics should be delayed until the safety, audit, and compliance foundations are mature.

See [`docs/mvp/mvp-1-scope.md`](docs/mvp/mvp-1-scope.md) for the MVP 1 product goal, target users, included features, exclusions, non-goals, success criteria, first wedge, and boundaries.

## Core principles

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

## Repository structure

```text
.
├── PRODUCT_ARCHITECTURE.md
├── README.md
├── docs/
│   ├── connectors/
│   │   └── connector-contract.md
│   ├── mvp/
│   │   └── mvp-1-scope.md
│   └── security/
│       └── safety-kernel-contract.md
└── packages/
    ├── README.md
    └── contracts/
        ├── README.md
        ├── VALIDATION.md
        ├── examples/
        │   ├── calendar.connector-manifest.example.json
        │   ├── file-cleanup.action-proposal.example.json
        │   ├── file-cleanup.approval-request.example.json
        │   ├── file-cleanup.audit-event.example.json
        │   ├── file-cleanup.rollback-metadata.example.json
        │   ├── file-metadata.connector-manifest.example.json
        │   ├── github.connector-manifest.example.json
        │   ├── homekit-matter-read-first.connector-manifest.example.json
        │   └── slack.connector-manifest.example.json
        ├── fixtures/
        │   └── README.md
        └── schemas/
            ├── action-proposal.schema.json
            ├── approval-request.schema.json
            ├── audit-event.schema.json
            ├── connector-manifest.schema.json
            └── rollback-metadata.schema.json
```

## Engineering execution docs

- [`docs/security/safety-kernel-contract.md`](docs/security/safety-kernel-contract.md): safety kernel purpose, risk classes, approval requirements, forbidden actions, proposal and approval payloads, audit events, rollback metadata, human override, and schema/example links.
- [`docs/connectors/connector-contract.md`](docs/connectors/connector-contract.md): connector purpose, required declaration fields, execution rules, MVP 1 connector examples, schema/example links, and read-first MVP posture.
- [`docs/mvp/mvp-1-scope.md`](docs/mvp/mvp-1-scope.md): MVP 1 scope, product goal, target users, included and excluded features, non-goals, success criteria, first wedge, and contract links.
- [`packages/README.md`](packages/README.md): shared package boundaries for future implementation work.
- [`packages/contracts/README.md`](packages/contracts/README.md): versioned JSON Schemas and synthetic examples for safety-kernel and connector contracts.

## Contracts status

[`packages/contracts/`](packages/contracts/README.md) is schema-only. It contains JSON Schemas, synthetic examples, fixture guidance, and validation expectations for future work. It does **not** contain runtime code, connector implementations, package managers, dependencies, generated types, validation scripts, CI workflows, app frameworks, or production tooling.

## Status

Early product architecture phase under Luca Dynamics.
