---
id: split-chart-explorer
title: "Modularize ChartExplorer responsibilities"
severity: HIGH
type: architecture
component: "src/pages/ChartExplorer.tsx"
status: open
estimate: L
dependencies: ["react-query-chart-data"]
---

## Rationale
The main analysis page has grown into a 1,500-line “god component”  mixing data orchestration, URL syncing, correlation logic, explanation rendering, CSV export, FLIP animations, and mobile layout concerns. This violates the layered approach described in docs/frontend/overview.md and makes the MVP hard to evolve.

## Evidence
- `src/pages/ChartExplorer.tsx` weighs in at 1,514 lines (`wc -l`), with long `useEffect` chains handling fetch planning (`src/pages/ChartExplorer.tsx:99`-`src/pages/ChartExplorer.tsx:366`) and large JSX trees (`src/pages/ChartExplorer.tsx:1000`+).
- Documentation flags ongoing maintenance pain (docs/frontend/components/pages/ChartExplorer.md) and notes outstanding TODOs tied to the file’s size.

## Impact
Continued feature work will be risky and slow because every change touches the same monolith. Testing is impractical, shared logic is duplicated, and onboarding new contributors is steep. Bugs like stale caches or inconsistent UI states emerge because responsibilities are tangled.

## Proposed Change
Split ChartExplorer into dedicated hooks (`useChartData`, `useExplain`, etc.) and presentational components (chart grid, explain overlay, share controls). Move fetch planning into reusable utilities aligned with React Query migration so data flow lives outside the view layer.

## Acceptance Criteria
- [ ] Core behaviors (data loading, explain overlay, sharing, custom pairs) are extracted into testable hooks or modules.
- [ ] View component stays under ~300 lines and focuses on layout/composition.
- [ ] Shared utilities are colocated in `src/lib` or `src/hooks` with unit tests.
- [ ] Documentation is updated to reflect the new module breakdown.

## Tasks
- [ ] Design a module breakdown covering data fetching, correlation, explain overlay, and UI rendering.
- [ ] Extract logic into new hooks/components with dedicated tests.
- [ ] Refactor ChartExplorer to consume the new abstractions.
- [ ] Update docs/frontend component references and diagrams.

## Rollout & Risk
Refactor touches critical UX—ship incrementally behind feature flags or target branches, with regression tests covering existing flows. Monitor error tracking for new runtime issues. Backout by reverting to the monolithic component if regressions surface.

## References
- docs/frontend/overview.md
- docs/frontend/components/pages/ChartExplorer.md
- src/pages/ChartExplorer.tsx
