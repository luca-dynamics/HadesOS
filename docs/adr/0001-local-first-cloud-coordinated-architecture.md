# ADR 0001: Local-First, Cloud-Coordinated Architecture

## Status

Accepted for the initial repository foundation.

## Context

HadesOS needs useful personal context, low-latency approvals, and privacy-preserving automation while still supporting multi-device sync, teams, and enterprise governance.

## Decision

Build the product around a local runtime that can observe local metadata, store encrypted memory, run safe local workflows, and collect approvals. Use cloud services for coordination, organization policy, sync, connector brokering when local execution is impossible, and enterprise administration.

## Consequences

Early engineering must separate local capabilities from cloud coordination. MVP 1 can work meaningfully on a single Mac before enterprise cloud features mature, but all data models must preserve future sync, tenant, audit, and policy requirements.

## Alternatives considered

A cloud-only assistant was rejected because it weakens privacy, offline usefulness, and user trust. A fully local-only product was rejected because SMB and enterprise coordination require shared policy, identity, and audit surfaces.
