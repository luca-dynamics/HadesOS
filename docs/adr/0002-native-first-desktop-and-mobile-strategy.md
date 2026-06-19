# ADR 0002: Native-First Desktop and Mobile Strategy

## Status

Accepted for the initial repository foundation.

## Context

The first product experience must feel calm, system-level, and trustworthy rather than like a browser dashboard or operations console.

## Decision

Prioritize a macOS-first desktop client and a focused mobile companion. Web admin remains a later organization-management surface, not the primary user experience.

## Consequences

Implementation should avoid committing to frontend frameworks in this foundation PR. Future client work should optimize for platform conventions, system permissions, local notifications, secure storage, and native approval flows.

## Alternatives considered

A web-first app was rejected for MVP 1 because it cannot provide the same system integration or trust posture. A mobile-only product was rejected because initial workflows require desktop file, calendar, app, and local runtime context.
