# data (`src/lib/data.ts`)

## Purpose
- Translates backend responses into the dashboard’s normalized `VDemDataPoint` shape and exposes helpers for fetching, sampling, and summarizing indicator data.

## API
- `fetchVDemData(countries, variable, startYear, endYear)` → `Promise<VDemDataPoint[]>` – orchestrates API selection (V-Dem vs IMF) and normalizes responses; falls back to synthetic data on failure.
- `getLatestValue(data, country)` → `number \| null` – highest-year observation for a given country.
- `generateSparklineData(data, country)` → `number[]` – ordered values for chart sparklines.

## Implementation Notes
- `transformApiData` resolves ambiguous variable names by consulting V-Dem and IMF mapping utilities; unmatched codes return an empty dataset and log a warning.
- Country IDs are reconciled against API `country_name` using normalized string comparisons and ISO3 fallbacks.
- Records API fetch plans for IMF requests with `setImfOrigin`, deciding between NEA and WEO endpoints when origin metadata is available.

## Usage Notes
- When integrating new backend endpoints, ensure they honour the `{ country_name, year, <metric> }` schema so `transformApiData` can extract values.
- TODO: Replace the `console.debug` branch for unmatched countries with structured telemetry once the backend taxonomy is finalized.
