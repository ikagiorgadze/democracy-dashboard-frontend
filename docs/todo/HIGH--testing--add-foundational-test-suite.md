---
id: add-foundational-tests
title: "Add foundational automated test suite"
severity: HIGH
type: testing
component: "repo-wide"
status: open
estimate: L
dependencies: []
---

## Rationale
Despite complex data orchestration and URL-driven workflows, the repository contains no unit, integration, or end-to-end tests. This contradicts the MVP’s need for maintainability and stability, especially as we harden API contracts and URL state per docs/frontend/state.md.

## Evidence
- `find src -name '*test*'` returns no files, indicating zero automated coverage.
- `package.json` exposes only `lint` and `docs` scripts; no `test` command or toolchain is configured.

## Impact
We cannot verify core behaviours (query state parsing, chart rendering, error handling) before deployments. Refactors risk introducing regressions, slowing delivery and eroding trust in the dashboard’s analytics.

## Proposed Change
Introduce a layered test strategy: unit tests for utilities (`url-state`, `data`, `api`), component tests for `ChartExplorer`/`ChartSidebar`, and at least one smoke E2E flow that exercises URL-deep linking. Standardise on Vitest or Jest plus React Testing Library, and configure CI to run the suite.

## Acceptance Criteria
- [ ] A `test` npm script executes automated tests locally and in CI.
- [ ] Unit tests cover critical helpers (`url-state`, `data` transformers, config).
- [ ] Component tests validate chart selection/rendering and error states.
- [ ] An E2E smoke test (Playwright/Cypress) confirms primary navigation and sharing flows.
- [ ] Coverage thresholds (or reports) are documented and enforced.

## Tasks
- [ ] Select and configure test runner(s) and supporting libraries.
- [ ] Write unit tests for lib modules handling parsing and data transforms.
- [ ] Write component tests for dashboard and chart interactions.
- [ ] Add an E2E smoke suite for core user journeys.
- [ ] Integrate tests into CI and document workflow in README/DEPLOYMENT notes.

## Rollout & Risk
Introduce the suite in stages to keep PRs reviewable. Monitor execution time in CI and adjust parallelism as needed. Backout plan is to disable new scripts temporarily if infrastructure issues arise.

## References
- docs/frontend/state.md
- package.json
- src/lib/url-state.ts
- src/pages/ChartExplorer.tsx
