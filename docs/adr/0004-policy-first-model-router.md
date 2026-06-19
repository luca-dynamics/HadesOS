# ADR 0004: Policy-First Model Router

## Status

Accepted for the initial repository foundation.

## Context

HadesOS will route requests across local, cloud, private, and deterministic systems while handling sensitive user and business data.

## Decision

The model router must evaluate policy before provider choice. Routing decisions must consider data classification, user consent, organization policy, risk class, latency, cost, capability, and audit requirements.

## Consequences

Model calls become governed events, not incidental implementation details. Engineers must preserve enough metadata to explain why a model or deterministic path was chosen.

## Alternatives considered

A provider-first router was rejected because it creates lock-in and weakens privacy controls. A simple cheapest-model router was rejected because cost is secondary to safety, data boundaries, and reliability.
