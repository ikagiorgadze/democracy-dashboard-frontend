---
id: validate-config
title: "Validate runtime API configuration"
severity: MEDIUM
type: architecture
component: "src/lib/api.ts"
status: open
estimate: S
dependencies: []
---

## Rationale
The API client defaults to `/api` and blindly trusts `import.meta.env.VITE_API_BASE_URL`. There is no central configuration validation despite the 12-factor style deployment hinted in docs/frontend/overview.md. Misconfigured environments will fail silently or point to the wrong backend.

## Evidence
`src/lib/api.ts:4`-`src/lib/api.ts:9`
```ts
const API_BASE_URL =
  (import.meta.env.VITE_API_BASE_URL && String(import.meta.env.VITE_API_BASE_URL).trim()) ||
  '/api';
```
No guardrails ensure HTTPS in production, detect missing variables, or expose configuration errors during startup.

## Impact
If staging or production forgets to set `VITE_API_BASE_URL`, the frontend issues requests to its own origin, leading to confusing 404s. Diagnosing the problem requires digging through network logs because the app never surfaces configuration errors to engineers or monitoring.

## Proposed Change
Introduce a config module that validates environment variables at build/start time (using Zod or a typed schema). Warn or fail fast when required variables are missing, enforce protocol/hostname rules per environment, and expose the resolved base URL via a single source.

## Acceptance Criteria
- [ ] A `config` module validates `VITE_API_BASE_URL` and other critical env vars.
- [ ] Invalid or missing config fails fast with a clear error message in development/CI.
- [ ] Production build emits structured logs when defaults are used.
- [ ] Documentation explains configuration requirements for each environment.

## Tasks
- [ ] Create `src/config.ts` (or similar) with schema validation.
- [ ] Replace ad-hoc env reads with the validated config module.
- [ ] Add tests covering valid/invalid configuration scenarios.
- [ ] Update deployment docs (DEPLOYMENT.md) with required variables.

## Rollout & Risk
Ensure CI and deployment pipelines export the expected variables before enabling strict validation. Roll out with feature flag or warning mode first, then switch to fail-fast once environments are clean. Backout by reverting to the previous permissive logic if necessary.

## References
- docs/frontend/overview.md
- DEPLOYMENT.md
- src/lib/api.ts
