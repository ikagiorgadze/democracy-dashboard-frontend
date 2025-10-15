# button (`src/components/ui/button.tsx`)

## Purpose
- Standardizes button styling and variants via `class-variance-authority` while keeping Radix Slot support for polymorphic rendering.

## Key Interactions
- Pulls variant classes from `button-variants.ts` and merges with any additional classes using `cn`.
- Supports the `asChild` pattern so components can render as links or other elements without losing button styles.

## Props
| Name | Type | Description | Default |
| --- | --- | --- | --- |
| `variant` | `VariantProps<typeof buttonVariants>['variant']` | Named style variant (`default`, `secondary`, etc.) defined in the variant helper. | Derived from variant helper |
| `size` | `VariantProps<typeof buttonVariants>['size']` | Size token controlling padding/typography. | Derived from variant helper |
| `asChild` | `boolean` | When true, renders a Radix `Slot` so the caller can supply the actual element. | `false` |
| `className` | `string` | Additional Tailwind classes merged into the computed variant. | — |
| `…props` | `React.ButtonHTMLAttributes<HTMLButtonElement>` | Native button attributes (type, disabled, etc.). | — |

## Usage Notes
- When `asChild` is active ensure the wrapped component forwards refs; otherwise focus handling breaks.
- Avoid applying Tailwind spacing classes directly; prefer configuring `button-variants.ts` so the design system stays centralized.
