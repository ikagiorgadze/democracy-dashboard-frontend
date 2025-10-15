# ChartCard (`src/components/ChartCard.tsx`)

## Purpose
- Summary tile for a single indicator on the dashboard landing page.
- Shows trend sparkline, latest values for up to three countries, and highlights directional cues.
- Acts as a navigation trigger into the full chart explorer for the chosen variable.

## Key Interactions
- Delegates trend visualization to `<Sparkline>` and passes the subset of data relevant to the indicator.
- Uses `getCountryById` and `getLatestValue` helpers to pair readings with readable country names.
- Applies semantic styling (`text-success-green`, `text-warning-orange`) based on the indicator's `direction` metadata.

## Props
| Name | Type | Description | Default |
| --- | --- | --- | --- |
| `variable` | `VDemVariable` | Metadata describing label, scale, unit, and direction for the indicator being rendered. | — |
| `data` | `VDemDataPoint[]` | Normalized time-series observations for the variable across selected countries. | — |
| `countries` | `string[]` | Country slugs to showcase in the sparkline and “latest values” badges. | — |
| `onClick` | `() => void` | Invoked when the card is clicked; parent typically uses this to navigate to `/chart`. | — |
| `selected` | `boolean` | Highlights the card when it corresponds to the active chart variable(s). | `false` |

## Usage Notes
- Truncates the “latest values” list to the first three countries and rolls the remainder into a `+N more` badge.
- When feeding IMF indicators, be sure `data` already reflects the normalized `VDemDataPoint` shape produced by `fetchVDemData`.
- The component is clickable as a single region; wrap with a focusable element if keyboard activation beyond `onClick` is required.
