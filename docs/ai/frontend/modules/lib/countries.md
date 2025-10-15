# countries (`src/lib/countries.ts`)

## Purpose
- Supplies the canonical list of country slugs, display names, and ISO-like identifiers used across the dashboard.
- Provides helpers for direct lookup and fuzzy search within the sidebar.

## API
- `COUNTRIES: Country[]`
- `getCountryById(id)` → `Country | undefined`
- `searchCountries(query)` → `Country[]`
- Type: `Country`

## Usage Notes
- Many historical polities (e.g., `baden`, `wurtemberg`) are included; filter upstream if you only want contemporary states.
- TODO: Populate the optional `region`/`flag` fields once assets are available to enhance grouping and display.
