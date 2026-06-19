# Contract Validation Plan

HadesOS contract examples should eventually be validated in CI against the JSON Schemas in [`schemas/`](schemas/). This document defines the intended validation behavior without adding package managers, dependencies, workflows, or scripts yet.

## Future CI expectations

A future validation job should:

1. Discover every `*.example.json` file in [`examples/`](examples/).
2. Select the matching schema by file suffix, for example `*.action-proposal.example.json` should validate against [`schemas/action-proposal.schema.json`](schemas/action-proposal.schema.json).
3. Validate JSON Schema Draft 2020-12 compliance.
4. Fail if an example contains unknown top-level fields, invalid enum values, missing required fields, malformed timestamps, or non-synthetic user data.
5. Report schema validation failures with the example path, schema path, and JSON pointer to the failing field.

## Privacy expectations

Validation should never require real user data. All examples and fixtures must remain synthetic, deterministic, and privacy-safe.

## Non-goals for this phase

This phase intentionally does not add:

- package managers
- dependency manifests
- validation scripts
- generated types
- CI workflows
- runtime implementation
