# hidden-variables (`src/lib/hidden-variables.ts`)

## Purpose
- Holds a curated allowlist of V-Dem variable codes that should be excluded from the sidebar menus (e.g., internal identifiers, free-text fields).

## API
- `HIDDEN_VARIABLE_CODES: Set<string>`

## Usage Notes
- `ChartSidebar` consults this set before surfacing variables; update the list whenever UX or backend feedback identifies additional fields to suppress.
- TODO: Document the rationale for each exclusion somewhere central (product or data glossary) so future contributors know which codes can be reinstated.
