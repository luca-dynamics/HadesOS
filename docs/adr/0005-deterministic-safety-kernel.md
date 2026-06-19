# ADR 0005: Deterministic Safety Kernel

## Status

Accepted for the initial repository foundation.

## Context

AI-generated plans can be useful but must not become an unchecked execution path for user data, workplace systems, devices, or physical environments.

## Decision

Create a deterministic safety kernel that classifies risk, enforces forbidden actions, checks policy, requires approvals, validates typed action proposals, and records audit decisions before executors run.

## Consequences

Agents can propose and explain actions, but typed deterministic executors perform side effects only after safety checks. This increases engineering discipline and slows some features, but it is core to trust.

## Alternatives considered

Letting agents call tools directly was rejected. Relying only on prompt instructions was rejected because safety requirements need inspectable, testable, deterministic enforcement.
