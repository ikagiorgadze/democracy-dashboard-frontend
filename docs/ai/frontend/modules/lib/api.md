# api (`src/lib/api.ts`)

## Purpose
- Centralized API client for V-Dem, IMF, and analytics endpoints, with runtime environment configuration and response normalization.

## API
- `ApiQueryRequest`: `{ countries: string[]; fields: string[]; start_year: number; end_year: number }`
- `apiService.query(request)` → `Promise<ApiDataPoint[]>` – POST `/v-dem/query`
- `apiService.queryImf(request, { isNea? })` → `Promise<ApiDataPoint[]>` – POST `/imf/query`
- `apiService.explainRelationships(payload: ExplainRequest)` → `Promise<{ explanation?: string } & Record<string, unknown>>` – POST `/analysis/relationships/explain`
- `apiService.getCorrelations(request: CorrelationsRequest)` → `Promise<CorrelationsResponse>` – GET `/analysis/relationships/datasets/correlations`
- Types exported for Explain/correlation requests and responses (`Index`, `CorrelationPair`, etc.).

## Usage Notes
- `API_BASE_URL` defaults to `/api` but respects `VITE_API_BASE_URL`; configure Vite's proxy or env vars accordingly.
- `query`/`queryImf` coerce `year` values that might arrive as `bigint`; downstream code can rely on plain numbers.
- TODO: Finalize the OpenAPI contract for `ExplainRequest` and `CorrelationsResponse` so the loose return typing (string vs JSON) can be narrowed and the TODO in `explainRelationships` removed.
- Errors are logged to `console.error` before rethrowing; wrap calls in try/catch if the UI needs silent failure handling.
