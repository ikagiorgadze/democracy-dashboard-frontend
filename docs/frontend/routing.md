# Routing Map

| Path | Component | Params | Loaders / Guards |
| --- | --- | --- | --- |
| `/` | `Dashboard` (`src/pages/Dashboard.tsx`) | Query string drives `QueryState` (`countries`, `from`, `to`, `var`, `vars`, etc.). | None |
| `/chart` | `ChartExplorer` (`src/pages/ChartExplorer.tsx`) | Same query params as `/`; no dynamic path params. | None |
| `/info/v-dem` | `VDemDatasetInfo` (`src/pages/VDemDatasetInfo.tsx`) | — | None |
| `/info/imf` | `IMFDatasetInfo` (`src/pages/IMFDatasetInfo.tsx`) | — | None |
| `*` | `NotFound` (`src/pages/NotFound.tsx`) | Receives unmatched pathname via `useLocation`. | Logs 404 to console; otherwise unguarded. |

## Notes
- Routes are defined in `src/App.tsx` inside a `<BrowserRouter>` with nested `<Routes>`.
- URL search parameters are converted to/from `QueryState` using `lib/url-state.ts`; changes propagate through React Router’s `useSearchParams`.
