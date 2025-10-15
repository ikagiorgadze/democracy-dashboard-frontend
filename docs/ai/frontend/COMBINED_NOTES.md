# Combined Notes

## Logs

### 01-inventory
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

### 02-static-refs
# Static Reference Generation – `npm run docs:build`
- Command: `npm run docs:build`
- Outcome: ❌ Failed during `typedoc` phase.
- Artifacts: `docs/typedoc` not generated; `docs/props.json` skipped because the chain aborted before `npm run docs:props`.
- Notable warning: glob `/src/index.tsx` missing (Typedoc config expects file that does not exist).
- Blocking error: `src/pages/ChartExplorer.tsx:257` – TS2345 (`readonly [string, VDemDataPoint[]]` not assignable to mutable tuple). Requires code fix or overload adaptation before static docs can compile.
- Next step: decide whether to adjust the reducer utilities to avoid returning `readonly` tuples or update Typedoc config; outside this documentation pass's scope.

## Component Docs Index
- `docs/ai/frontend/components/App.md`
- `docs/ai/frontend/components/components/ChartCard.md`
- `docs/ai/frontend/components/components/ChartSidebar.md`
- `docs/ai/frontend/components/components/GlobalHeader.md`
- `docs/ai/frontend/components/components/Sparkline.md`
- `docs/ai/frontend/components/components/ui/button.md`
- `docs/ai/frontend/components/components/ui/checkbox.md`
- `docs/ai/frontend/components/components/ui/help-icon.md`
- `docs/ai/frontend/components/components/ui/input.md`
- `docs/ai/frontend/components/components/ui/label.md`
- `docs/ai/frontend/components/components/ui/select.md`
- `docs/ai/frontend/components/components/ui/sonner.md`
- `docs/ai/frontend/components/components/ui/toaster.md`
- `docs/ai/frontend/components/components/ui/toast.md`
- `docs/ai/frontend/components/components/ui/tooltip.md`
- `docs/ai/frontend/components/main.md`
- `docs/ai/frontend/components/pages/ChartExplorer.md`
- `docs/ai/frontend/components/pages/Dashboard.md`
- `docs/ai/frontend/components/pages/IMFDatasetInfo.md`
- `docs/ai/frontend/components/pages/NotFound.md`
- `docs/ai/frontend/components/pages/VDemDatasetInfo.md`

## Module Docs Index
- `docs/ai/frontend/modules/components/ui/button-variants.md`
- `docs/ai/frontend/modules/components/ui/sonner-toast.md`
- `docs/ai/frontend/modules/hooks/use-toast.md`
- `docs/ai/frontend/modules/lib/api.md`
- `docs/ai/frontend/modules/lib/countries.md`
- `docs/ai/frontend/modules/lib/data.md`
- `docs/ai/frontend/modules/lib/hidden-variables.md`
- `docs/ai/frontend/modules/lib/imf-codes.md`
- `docs/ai/frontend/modules/lib/imf-origin.md`
- `docs/ai/frontend/modules/lib/measure-index.md`
- `docs/ai/frontend/modules/lib/url-state.md`
- `docs/ai/frontend/modules/lib/utils.md`
- `docs/ai/frontend/modules/lib/variable-codes.md`
- `docs/ai/frontend/modules/lib/variable-mappings.md`
- `docs/ai/frontend/modules/lib/variables.md`
- `docs/ai/frontend/modules/types/request.md`
