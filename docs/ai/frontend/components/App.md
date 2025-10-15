# App (`src/App.tsx`)

## Purpose
- Root component wiring together global providers (React Query, tooltip context), top-level layout, and React Router routes.
- Synchronizes URL search parameters with the shared `QueryState` so navigation and filters stay in lockstep.

## Key Interactions
- Creates a singleton `QueryClient` and provides it via `QueryClientProvider` (foundation for data fetching hooks if introduced later).
- Wraps the app with `TooltipProvider`, shadcn `Toaster`, and `sonner` `Toaster` to enable both toast systems.
- Defines route table inside `<BrowserRouter>`:
  - `/` → `<Dashboard />`
  - `/chart` → `<ChartExplorer />`
  - `/info/v-dem` → `<VDemDatasetInfo />`
  - `/info/imf` → `<IMFDatasetInfo />`
  - `*` → `<NotFound />`
- Keeps an internal `currentQuery` state derived from `useSearchParams`; updates both state and URL via `stateToUrlParams` when `handleQueryChange` runs.
- Auto-redirects from `/` to `/chart` when the user selects a variable so the chart explorer opens immediately.

## Props
- The component exports as default and accepts no props; `AppContent` receives state from the router hooks.

## Usage Notes
- Because `handleQueryChange` sets `currentQuery` and manipulates the router, ensure upstream callers pass complete `QueryState` snapshots (not partial diffs).
- When adding new routes, update both the `Routes` block and documentation in `docs/ai/frontend/routing.md`.
