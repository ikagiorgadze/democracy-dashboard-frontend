# Frontend Overview

## Architecture
- Vite + React 18 (TypeScript) with React Router 6 managing navigation.
- TanStack Query is provisioned for data fetching; requests currently use a handcrafted API client.
- UI primitives come from shadcn/Radix with Tailwind CSS styling, while charting relies on `recharts`.
- Shared state centers on the URL-driven `QueryState`, keeping deep links in sync with user selections.

## Working Locally
- Install dependencies with `npm install`.
- `npm run dev` starts the Vite dev server; `npm run preview` serves the production build created by `npm run build`.
- `npm run lint` runs ESLint.
- `npm run docs:build` should produce Typedoc content once the `Promise.all` tuple type in `src/pages/ChartExplorer.tsx` is adjusted; track progress in [static-reference.md](notes/static-reference.md).

## Feature Entry Points
- Dashboard entry: `src/App.tsx` wraps global providers and mounts React Router routes.
- Landing experience: `src/pages/Dashboard.tsx`.
- Core exploration workflow: `src/pages/ChartExplorer.tsx`.
- Dataset explainers: `src/pages/VDemDatasetInfo.tsx`, `src/pages/IMFDatasetInfo.tsx`.
- Fallback routing: `src/pages/NotFound.tsx`.

## Key Concepts
- Sidebar selections feed into `QueryState`, serialized by `src/lib/url-state.ts`.
- Data fetching happens through `src/lib/api.ts` and `src/lib/data.ts`, which normalise responses for charts.
- Toast notifications and IMF dataset origin tracking live in module-scoped stores (`src/hooks/use-toast.ts`, `src/lib/imf-origin.ts`).

## Additional References
- [Routing Map](routing.md)
- [State Map](state.md)
- [API Usage](api-usage.md)
- [Component Reference](components)
- [Module Reference](modules)
