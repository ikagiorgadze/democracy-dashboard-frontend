# checkbox (`src/components/ui/checkbox.tsx`)

## Purpose
- Styled wrapper around Radix Checkbox used for multi-select filters (countries, dataset toggles).

## Key Interactions
- Combines Radix state classes with Tailwind tokens to convey checked/disabled states.
- Uses Lucide’s `Check` icon inside the indicator slot for visual confirmation.

## Props
| Name | Type | Description | Default |
| --- | --- | --- | --- |
| `className` | `string` | Additional Tailwind classes appended to the base square control. | — |
| `…props` | `React.ComponentPropsWithoutRef<typeof CheckboxPrimitive.Root>` | Standard checkbox props (`checked`, `onCheckedChange`, etc.). | — |

## Usage Notes
- Because Radix returns `boolean \| "indeterminate"`, remember to coerce to `boolean` when syncing with traditional HTML inputs.
- The component is `forwardRef` enabled, so hook form libraries can register it as a controlled field.
