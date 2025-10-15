---
id: react-query-chart-data
title: "Migrate chart data fetching to React Query"
severity: MEDIUM
type: architecture
component: "src/pages/ChartExplorer.tsx"
status: open
estimate: L
dependencies: ["harden-url-state"]
---

## Rationale
Documentation notes that React Query is provisioned but unused, and manual loaders should migrate once contracts stabilise (docs/frontend/state.md). The current bespoke loader in `ChartExplorer` reimplements caching, deduping, and lifecycle management, making the component hard to maintain and error-prone.

## Evidence
`src/pages/ChartExplorer.tsx:99`-`src/pages/ChartExplorer.tsx:310`
```ts
useEffect(() => {
  let cancelled = false;
  const loadData = async () => {
    ...
    const planResults = await Promise.all(
      plan.variables.map(async (v) => {
        const result = await fetchVDemData(...);
        return [v, result] as const;
      })
    );
    ...
    setDataByVar(prev => { ... });
    setChartDataByVar(prevChart => { ... });
  };
  loadData();
  return () => { cancelled = true; };
}, [ ... ]);
```
All caching, race protection, and deduplication are hand-coded, bypassing the `QueryClient` set up in `App.tsx`.

## Impact
The custom loader increases bug surface area (e.g., stale caches when navigating, no deduping across components, no automatic retries/backoff) and blocks straightforward error handling. It also prevents us from leveraging React Query's devtools and caching strategies, slowing iteration.

## Proposed Change
Model each variable/country/year request as a React Query (batched with `useQueries` or `queryClient.fetchQuery`) keyed by state, and move cache shaping logic into selectors. This removes manual state mutation, enables retries, and lets us share cached data with other views.

## Acceptance Criteria
- [ ] Chart data is fetched through React Query hooks with appropriate cache keys.
- [ ] Loading, error, and success states derive from React Query metadata instead of manual booleans.
- [ ] Redundant local caches (`dataByVar`, `chartDataByVar`, `loadedDataRef`) are removed.
- [ ] Integration tests confirm charts render after cache hits and error states display correctly.

## Tasks
- [ ] Design query keys per variable/country/year range and implement hooks in `src/lib/data.ts`.
- [ ] Refactor `ChartExplorer` to consume the new hooks and simplify state.
- [ ] Add tests (component or hook-level) covering loading->success/error flows.
- [ ] Update documentation describing the new data fetching approach.

## Rollout & Risk
Refactor touches core UX; ship behind a feature flag and test extensively on staging. Monitor cache sizes and memory usage after rollout. Backout plan: revert to previous loader if critical regressions emerge.

## References
- docs/frontend/state.md
- src/App.tsx
- src/pages/ChartExplorer.tsx
