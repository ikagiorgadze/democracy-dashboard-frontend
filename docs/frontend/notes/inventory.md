# Inventory – Democracy Dashboard Frontend

## Components
- `src/components/GlobalHeader.tsx` – top-level navigation/search header driving query state updates.
- `src/components/ChartCard.tsx` – card wrapper around chart visualizations and metadata.
- `src/components/ChartSidebar.tsx` – sidebar controls for variable/date selection.
- `src/components/Sparkline.tsx` – compact mini-chart for summarizing time-series trends.
- `src/components/ui/` – shared UI primitives (button, checkbox, input, label, select, tooltip, toaster, sonner toast bridge) plus variant helpers.

## Pages
- `src/pages/Dashboard.tsx` – landing page; exposes dataset variable browsing controls.
- `src/pages/ChartExplorer.tsx` – full chart exploration surface driven by URL/query state.
- `src/pages/VDemDatasetInfo.tsx` & `src/pages/IMFDatasetInfo.tsx` – static dataset documentation screens.
- `src/pages/NotFound.tsx` – fallback for unknown routes.

## Hooks
- `src/hooks/use-toast.ts` – wrapper around `sonner` and shadcn toaster instances.

## Routing Entrypoints
- `src/App.tsx` – configures React Router routes, query sync, and shared providers (React Query, Tooltip, Toast).
- `src/main.tsx` – Vite entry; mounts `<App />` into the DOM.

## State & Utilities
- `src/lib/url-state.ts` – query-string serialization, default state, conversion helpers.
- `src/lib/api.ts` – API helper for fetching dataset metadata and time series.
- `src/lib/data.ts` – data shape adapters for charting & derived metrics.
- `src/lib/variables.ts`, `src/lib/variable-mappings.ts`, `src/lib/variable-codes.ts`, `src/lib/hidden-variables.ts`, `src/lib/measure-index.ts`, `src/lib/imf-codes.ts`, `src/lib/imf-origin.ts`, `src/lib/countries.ts` – static metadata and lookup utilities.
- `src/lib/utils.ts` – assorted formatting/helpers (numbers, arrays, colors).

## Styles & Assets
- `src/index.css` – Tailwind directives and global styles.
- JSON assets: `src/translations.json`, `src/weo-indicator-series-codes.json`, `src/nea-indicator-series-codes.json`.
- Type declarations: `src/types/request.ts`, `src/vite-env.d.ts`.

