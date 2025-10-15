# label (`src/components/ui/label.tsx`)

## Purpose
- Radix UI label primitive wrapped with Tailwind variants used throughout the app’s forms and filter panels.

## Key Interactions
- Uses `class-variance-authority` to expose future style variants while keeping current styles consistent.
- Forwards refs and props to `@radix-ui/react-label` to preserve accessibility features like `htmlFor`.

## Props
| Name | Type | Description | Default |
| --- | --- | --- | --- |
| `className` | `string` | Extra Tailwind classes merged with the base style. | — |
| `…props` | `React.ComponentPropsWithoutRef<typeof LabelPrimitive.Root>` | Standard Radix label props such as `htmlFor` and event handlers. | — |

## Usage Notes
- Pair with input components using matching `id` / `htmlFor` values to ensure screen-reader announcement.
- The component already accounts for the disabled peer state (via `peer-disabled` selectors); no additional styling necessary.
