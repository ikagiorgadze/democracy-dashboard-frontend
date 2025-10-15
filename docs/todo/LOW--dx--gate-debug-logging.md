---
id: gate-debug-logs
title: "Gate debug logging behind environment checks"
severity: LOW
type: dx
component: "src/pages/ChartExplorer.tsx"
status: open
estimate: S
dependencies: []
---

## Rationale
The MVP ships with emoji-rich `console.log` statements in core render paths. Documentation emphasises shared state fidelity (docs/frontend/state.md), but these logs run in production, clutter browser consoles for users, and leak internal fetch details.

## Evidence
`src/pages/ChartExplorer.tsx:213`
```ts
console.log('Incremental loading analysis:', { ... });
```
`src/pages/ChartExplorer.tsx:245`
```ts
console.log(`Fetching ${plan.reason}: ...`);
```
`src/pages/ChartExplorer.tsx:856`
```ts
console.log('Link copied to clipboard');
```

## Impact
Uncontrolled logging harms UX for analysts embedding the dashboard, makes debugging harder by mixing signal and noise, and reveals internal reasoning to end users. It also increases risk of accidentally logging sensitive payloads.

## Proposed Change
Wrap diagnostic logging behind `if (import.meta.env.DEV)` (or remove it entirely) and route operational telemetry through a structured logger when we need observability. Provide user-facing feedback (toasts/snackbars) instead of relying on console messages.

## Acceptance Criteria
- [ ] All debug logs are removed or guarded so they do not execute in production builds.
- [ ] User feedback (e.g., copy-to-clipboard confirmation) uses UI patterns instead of console statements.
- [ ] ESLint rule (`no-console`) or custom lint config enforces the policy outside development-only blocks.

## Tasks
- [ ] Audit `src/pages/ChartExplorer.tsx` (and related files) for `console.*`.
- [ ] Wrap necessary diagnostics in dev-only guards or replace with structured logging.
- [ ] Enable/adjust lint rule to catch future console usage.
- [ ] Document logging policy for contributors.

## Rollout & Risk
Low risk—ensure developer ergonomics remain by keeping dev-only logs available. Backout simply reinstates prior logging if needed.

## References
- docs/frontend/state.md
- eslint.config.js
- src/pages/ChartExplorer.tsx
