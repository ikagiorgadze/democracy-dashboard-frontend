# variables (`src/lib/variables.ts`)

## Purpose
- Enumerates V-Dem categories, subcategories, and curated indicator metadata consumed by the sidebar and dashboard tiles.
- Provides helper functions for looking up categories, subcategories, and variable definitions.

## API
- Types: `VDemCategory`, `VDemSubcategory`, `VDemVariable`
- Data: `SUBCATEGORIES`, `VDEM_VARIABLES`, `CATEGORIES`
- Helpers:
  - `getSubcategoriesByCategory(category)`
  - `getVariablesBySubcategory(subcategoryId)`
  - `getVariablesByCategory(category)`
  - `getVariableById(id)`
  - `getSubcategoryById(id)`

## Usage Notes
- The exposed helpers rely on in-memory arrays; any future lazy-loading should keep the exported function signatures identical.
- When expanding the dataset, keep metadata synchronized with `variable-mappings.ts` and `variable-codes.ts` to avoid mismatch between sidebar labels and API codes.
