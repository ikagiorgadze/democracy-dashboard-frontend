---
id: test-chart-explorer
title: "Add ChartExplorer interaction tests"
severity: MEDIUM
type: testing
component: "src/pages/ChartExplorer.tsx"
status: open
estimate: L
dependencies: ["react-query-chart-data", "split-chart-explorer", "add-foundational-tests"]
---

## Rationale
The core analysis surface manages mobile/desktop layouts, pairing workflows, explain overlays, CSV downloads, and share links, but no automated tests confirm these flows. Documentation calls out complex cache invalidation and UI states (docs/frontend/components/pages/ChartExplorer.md), yet everything is manual.

## Evidence
- `ChartExplorer` contains numerous interactive branches (e.g., `toggleChartPairing`, `removeCustomPair`, `handleShareLink`, `runExplainForCountries`) between `src/pages/ChartExplorer.tsx:720`-`src/pages/ChartExplorer.tsx:1210` with zero corresponding tests.
- `find src -name '*test*'` shows no existing component coverage.

## Impact
UX regressions (e.g., custom pair removal, explain overlays not opening, clipboard failures) go unnoticed until users report them. Refactors like the planned React Query migration risk breaking core workflows without any safety net.

## Proposed Change
Once the component is modularised, add React Testing Library (or similar) tests exercising the major user journeys: selecting variables, pairing charts, triggering share/explain actions, and verifying responsive behaviour gates. Mock APIs and clipboard to assert side effects.

## Acceptance Criteria
- [ ] Tests cover variable selection, pair creation/removal, and ensure `onQueryChange` receives correct payloads.
- [ ] Explain overlay tests simulate successful and failing API responses.
- [ ] Share action tests verify clipboard writes (mocked) and UI feedback states.
- [ ] CSV download logic is validated without touching the real filesystem (mock `URL.createObjectURL`).

## Tasks
- [ ] Break ChartExplorer into testable subcomponents/hooks (dependency).
- [ ] Set up component testing utilities (RTL, user-event).
- [ ] Implement interaction tests for desktop and mobile breakpoints.
- [ ] Document testing guidelines alongside component docs.

## Rollout & Risk
Needs coordination with refactors; keep tests resilient to future layout adjustments by targeting roles/labels. Backout by temporarily skipping new tests if refactor churn makes them unstable.

## References
- docs/frontend/components/pages/ChartExplorer.md
- src/pages/ChartExplorer.tsx
