# API Usage (Frontend Observed)

| Call Site | HTTP Method & Endpoint | Request Payload | Response Handling | Notes / TODO |
| --- | --- | --- | --- | --- |
| `src/lib/api.ts:88` (`apiService.query`) | `POST ${API_BASE_URL}/v-dem/query` | `{ countries: string[]; fields: string[]; start_year: number; end_year: number }` | Expects JSON array of objects with `country_name`, `year`, and metric fields; coerces `year` from `bigint` if necessary. | TODO: Confirm final schema via OpenAPI (including additional metadata fields, error envelope). |
| `src/lib/api.ts:118` (`apiService.queryImf`) | `POST ${API_BASE_URL}/imf/query` | Same base payload, optionally extended with `{ isNea: true }`. | Same normalization as V-Dem query. | TODO: Document how IMF endpoint signals units/currency to display in UI. |
| `src/lib/api.ts:148` (`apiService.explainRelationships`) | `POST ${API_BASE_URL}/analysis/relationships/explain` | `{ indexA: Index; indexB: Index; country: string; execute?: boolean }` where `Index` carries `{ name: string; data: { year: number; observation: number }[] }`. | Reads `Content-Type`; attempts JSON parse, otherwise treats body as plain text. Returns `{ explanation?: string }`. | TODO: Align response contract (string vs JSON) with backend; currently falls back to raw text. |
| `src/lib/api.ts:196` (`apiService.getCorrelations`) | `GET ${API_BASE_URL}/analysis/relationships/datasets/correlations?country=…` + query params | Query string includes `country`, `type`, `dataset1`, `dataset2`, optional `minObservations`, `limit`. | Expects JSON object `{ correlations: CorrelationPair[] }`. | TODO: Validate correlation pair fields (`indexA`, `indexB`, `r`, `n`, `p_value`) once backend spec is published. |

## Callers
- `fetchVDemData` selects between `query` and `queryImf` based on variable code patterns/origin.
- `ChartExplorer` triggers `getCorrelations` and `explainRelationships` when users opt into those workflows.
- No other direct `fetch`/`axios` calls were detected.
