# Dashboard (`src/pages/Dashboard.tsx`)

## Purpose
- Landing page experience that introduces the Democracy Dashboard and showcases example indicators via `ChartCard` tiles.
- Bridges the homepage and chart explorer by precomputing demo data and deep-linking into `/chart` with the user’s current filter context.

## Key Interactions
- Computes `effectiveCountries`, falling back to a sample trio when the user has not selected any countries yet.
- Fetches sample datasets for a curated list of V-Dem variables with `fetchVDemData`, storing results keyed by variable id in `cardData`.
- Uses `buildChartUrl` to craft chart explorer links that preserve year ranges and countries, overriding the variables array to align with multi-chart behavior.
- Displays loading skeleton with animated spinner while async data resolves.

## Props
| Name | Type | Description | Default |
| --- | --- | --- | --- |
| `currentQuery` | `QueryState` | Global query state mirrored in the URL. | — |
| `onQueryChange` | `(query: QueryState) => void` | Callback for pushing query updates upstream (currently only used indirectly via navigation). | — |

## Usage Notes
- The effect that populates `cardData` deliberately omits `currentQuery` dependencies for `variables` to avoid infinite loops; keep the ESLint suppression intact or refactor with care.
- When the user clicks a card and no countries are selected, the handler injects `SAMPLE_COUNTRIES` to ensure the chart page has data to render.
- Consider memoizing `variablesForCards` if the list grows substantially, although the static array render is currently cheap.
