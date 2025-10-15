# ChartSidebar (`src/components/ChartSidebar.tsx`)

## Purpose
- Primary filter surface for the chart explorer: manages country selection, category/subcategory navigation, and variable pickers across V-Dem and IMF datasets.
- Drives year range controls, correlation workflows, and measure reveal hooks used by the main chart grid.
- Offers extensive keyboard support and accessibility affordances for deep hierarchies.

## Key Interactions
- Synchronizes local UI state with the canonical `QueryState`, calling `onQueryChange` after every confirmed edit (countries, variables, years, correlations).
- Builds hierarchical data from `CATEGORIES`, `getSubcategoriesForCategory`, and IMF mappings to render a virtualized navigation tree with expand/collapse state tracked via `Set`s.
- Integrates with `apiService.getCorrelations` to auto-fetch dataset correlations when the user selects two datasets and a country; results are stored locally and surfaced in the sidebar panel.
- Uses `registerReveal` to expose a callback that lets the main chart surface request a specific measure be scrolled into view and expanded.
- Persists IMF origin metadata with `setImfOrigin` so downstream fetches know whether to hit the WEO or NEA endpoint.
- Implements debounced suggestion search (`measureSearch` → `filteredSuggestions`) across both V-Dem and IMF codebases.

## Props
| Name | Type | Description | Default |
| --- | --- | --- | --- |
| `currentQuery` | `QueryState` | Canonical selection state mirrored in the URL and chart explorer. | — |
| `onQueryChange` | `(q: QueryState) => void` | Callback that persists sidebar mutations back to the application state. | — |
| `registerReveal` | `(fn: ((code: string, displayLabel?: string) => void) \| null) => void` | Optional channel for passing a “reveal measure” helper up to parents; invoked during mount/unmount. | — |

## Usage Notes
- Maintains several parallel `Set` instances (`expandedDatasets`, `expandedCategories`, `expandedSubcats`, etc.) to control disclosure state—always clone before mutating to keep React state updates predictable.
- Year inputs keep separate uncontrolled text state (`fromYearInput`, `toYearInput`) to support partial entry; `commitYear` clamps ranges between 1800 and the current year.
- Correlation fetches guard against duplicate requests with a `correlationsRequestInProgress` ref; reset it whenever parameters change to avoid stale locks.
- TODO: Confirm the structure of `CorrelationPair` returned by the backend OpenAPI once available—currently inferred fields (`indexA`, `indexB`, `r`, `n`, `p_value`) should be validated.
