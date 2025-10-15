# ChartExplorer (`src/pages/ChartExplorer.tsx`)

## Purpose
- Main analytical surface for comparing democracy and economic indicators across countries.
- Orchestrates data fetching, chart rendering, correlation analysis, explanation overlays, and sharing workflows tied to the URL-driven `QueryState`.

## Key Interactions
- Reads and writes URL search params via `useSearchParams`; every `onQueryChange` call mirrors state into the browser history so deep links stay stable.
- Maintains an incremental fetch planner that compares requested variables/countries/year ranges against a memoized cache (`loadedDataRef`) to avoid redundant network calls. Fetch plans are executed in batches with `fetchVDemData`.
- Normalizes raw API responses into chart-friendly rows (`ChartRow`) keyed by year and country, ensuring recharts receives stable arrays for `<LineChart>` instances.
- Integrates with `<ChartSidebar />` through `registerReveal` so sidebar selections can scroll/expand specific measures from the main grid.
- Supports correlation workflows:
  - Renders backend-provided correlation pairs (from `currentQuery.correlationPairs`).
  - Lets users create custom pairs in-app; paired variables are withheld from single-variable charts to avoid duplication.
- Provides “Explain” overlays by calling `apiService.explainRelationships` per country and parsing markdown-like responses into JSX blocks.
- Implements shareable URLs via `navigator.clipboard.writeText`, with UI feedback stored in `copiedVar`.
- Applies FLIP-style layout adjustments in `useLayoutEffect` to smooth reordering when variables are added/removed.

## Props
| Name | Type | Description | Default |
| --- | --- | --- | --- |
| `currentQuery` | `QueryState` | Canonical state controlling selected countries, variables, pairs, chart options, etc. | — |
| `onQueryChange` | `(query: QueryState) => void` | Upstream callback for persisting edits and triggering URL updates. | — |

## Usage Notes
- Data cache invalidation relies on tracking removed variables; when extending query state make sure to clear associated entries so stale charts disappear.
- `Promise.all` returns `readonly` tuples, which currently surface as a TS2345 during Typedoc builds. TODO: adjust the `planResults` spread (`allFetchResults.push(...planResults as [string, VDemDataPoint[]][])`) or refactor to mutable arrays so docs generation succeeds.
- The incremental loader logs fetch plans to the console (`Incremental loading analysis`); keep this logging lightweight or gate behind `import.meta.env.DEV` if performance becomes a concern.
- When adding new query dimensions (e.g., smoothing, normalization) ensure they are encoded/decoded in `url-state.ts` so share links capture the full state.
