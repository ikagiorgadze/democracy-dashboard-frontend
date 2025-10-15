**Architecture**
- Vite + React 18 (TypeScript) with React Router 6 driving navigation and TanStack Query provisioned for future data fetching.
- UI primitives are sourced from shadcn/Radix with Tailwind CSS styling; charts leverage `recharts`.
- State is URL-centric (`QueryState`) so routes remain shareable; see `docs/ai/frontend/state.md` for the full map.

**Run / Build / Test**
- `npm install` (if deps change), then `npm run dev` for local development at the default Vite port.
- `npm run build` emits production assets; `npm run preview` serves the build locally.
- `npm run lint` runs ESLint.
- Documentation build (`npm run docs:build`) currently fails: Typedoc surfaces `TS2345` in `src/pages/ChartExplorer.tsx` because `Promise.all` returns a readonly tuple. Adjust the spread or suppress the readonly typing before rerunning.

**Routing Overview**
- High-level routes: `/` → Dashboard, `/chart` → ChartExplorer, `/info/v-dem`, `/info/imf`, and `*` → NotFound.
- URL query params encode filter state (`countries`, `from`, `to`, `var`, `vars`, correlation metadata, etc.).
- Full details in `docs/ai/frontend/routing.md`.

**State Overview**
- Shared query state lives in `AppContent` and synchronizes with the URL; sidebar and explorer components push updates via `onQueryChange`.
- Local component state handles layout toggles, correlation results, and incremental data caches.
- Toasts use a bespoke reducer (`useToast`); IMF origin tracking relies on a module-scoped map.
- Deeper discussion in `docs/ai/frontend/state.md`.

**Component Conventions**
- Each React component and module now has a mirrored markdown file under `docs/ai/frontend/components` or `docs/ai/frontend/modules`.
- Place new UI components under `src/components/...` and mirror their documentation in `docs/ai/frontend/components/<same-path>.md` covering purpose, interactions, and props.
- Utilities, hooks, or data modules belong in `src/lib` / `src/hooks` / `src/components/ui` and should receive companion docs beneath `docs/ai/frontend/modules/<same-path>.md`.

**API Usage Summary**
- All network traffic flows through `apiService` (`/api/v-dem/query`, `/api/imf/query`, `/api/analysis/relationships/explain`, `/api/analysis/relationships/datasets/correlations`).
- Response normalization currently assumes `{ country_name, year, … }`; TODO: reconcile with the backend OpenAPI once published so typings can be tightened and docs build succeeds without manual guards.
- Endpoint call breakdown with TODOs: `docs/ai/frontend/api-usage.md`.
