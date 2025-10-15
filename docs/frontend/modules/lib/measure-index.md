# measure-index (`src/lib/measure-index.ts`)

## Purpose
- Precomputes reverse lookups from variable codes and labels back to their category/subcategory hierarchy, enabling sidebar reveal and breadcrumb features.

## API
- `getMeasurePathByCode(code)` → `{ category, subcategoryLabel, variableLabel } | undefined`
- `getMeasurePathByLabel(label)` → `{ category, subcategoryLabel } | undefined`
- `hasMeasureCode(code)` → `boolean`
- Type: `MeasurePath`

## Usage Notes
- The index is built eagerly at module load; if the mappings become too large, consider deferring construction until first use.
- Ensure updates to `variable-mappings.ts` and `variable-codes.ts` remain in sync; missing entries will cause `undefined` reveal lookups.
