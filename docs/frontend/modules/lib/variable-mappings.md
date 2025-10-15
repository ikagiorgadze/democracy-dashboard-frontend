# variable-mappings (`src/lib/variable-mappings.ts`)

## Purpose
- Maps high-level V-Dem categories to their subcategories and lists the human-readable variable names within each subcategory.
- Powers the hierarchical navigation tree in `ChartSidebar` and assists `measure-index.ts` when resolving “reveal” requests.

## API
- `CATEGORY_SUBCATEGORIES: Record<VDemCategory, string[]>`
- `SUBCATEGORY_VARIABLES: Record<VDemCategory, Record<string, string[]>>`

## Usage Notes
- Maintain parity between the string labels here and the subcategory ids defined in `variables.ts`; mismatches will cause lookup failures when building lists.
- If the dataset size becomes an issue, consider splitting the mappings per category and lazy-loading them, but preserve the exported shapes for compatibility.
