# State Map

## Query State
- **Source**: `src/lib/url-state.ts`
- **Shape**: `QueryState` tracks countries, year range, selected variables, correlation datasets/pairs, and chart preferences.
- **Lifecycle**: Initialized from `urlParamsToState` in `AppContent`. Mutations originate from `ChartSidebar`, `ChartExplorer`, and `Dashboard`, then flow through `handleQueryChange` which updates both React state and the router search params.

## React Query
- **Provider**: `QueryClientProvider` wraps the app in `src/App.tsx`.
- **Usage**: No hooks currently invoke `useQuery`; the provider scaffolds future data-fetching logic.
- **Next Steps**: Consider migrating manual fetches in `ChartExplorer` to React Query for caching and deduplication once backend contracts solidify.

## Local Component State
- `ChartExplorer`: Manages incremental data caches (`dataByVar`, `chartDataByVar`), UI toggles (mobile filters, explain overlays), and pairing selections.
- `ChartSidebar`: Tracks expanded tree nodes, search inputs, correlation results, and mobile affordances.
- `Dashboard`: Stores example card data while fetching asynchronous V-Dem metrics.
- `GlobalHeader`: stateless aside from navigation callbacks.

## Custom Stores & Hooks
- `useToast` (`src/hooks/use-toast.ts`): Module-level reducer with listener subscriptions; exposes `toast` and `dismiss`. Limited to a single active toast (`TOAST_LIMIT = 1`).
- `imf-origin` map: Module-scoped `Map` remembering whether an IMF code came from the WEO or NEA dataset to inform subsequent API calls.

## Async Data Flow
- All remote calls route through `apiService` (`src/lib/api.ts`). `ChartExplorer` batches calls to `/v-dem/query`, `/imf/query`, `/analysis/relationships/explain`, and `/analysis/relationships/datasets/correlations`.
- Error handling currently logs to the console and, where relevant, falls back to synthetic data (`fetchVDemData`).
- TODO: Align the correlations and explain endpoints with a published OpenAPI spec so clients can rely on typed responses and potentially integrate with React Query caching.
