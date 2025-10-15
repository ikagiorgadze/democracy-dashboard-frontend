# Sparkline (`src/components/Sparkline.tsx`)

## Purpose
- Lightweight SVG sparkline visualizing up to two country time series for a selected indicator.
- Provides a compact overview used inside `ChartCard` without introducing a charting dependency.

## Key Interactions
- Filters incoming `VDemDataPoint` records to the requested `variable` before deriving ranges.
- Normalizes min/max values to the `0–100` SVG coordinate space so lines stay vertically proportional.
- Limits rendering to the first two countries to keep the SVG legible in small footprints.

## Props
| Name | Type | Description | Default |
| --- | --- | --- | --- |
| `data` | `VDemDataPoint[]` | Normalized time-series points (country, year, value) for multiple countries. | — |
| `variable` | `string` | Identifier used to filter the shared dataset down to the indicator the sparkline represents. | — |
| `countries` | `string[]` | Country slugs to render; the component renders at most the first two. | — |

## Usage Notes
- Returns a “No data” placeholder when the filtered dataset is empty, so callers do not need to special-case empty states.
- When all values are identical the range collapses to zero; the component falls back to a centered horizontal line via the `range > 0` guard.
- If you pass more than two countries only the first two (in incoming order) will render; reorder the array upstream to control priority.
