# input (`src/components/ui/input.tsx`)

## Purpose
- Tailwind-themed text input aligned with the rest of the shadcn UI primitives.

## Key Interactions
- Wraps a native `<input>` and merges incoming `className` with the standard set of focus and disabled styles.
- Forwards refs so higher-level forms can imperatively focus or integrate with libraries like React Hook Form.

## Props
| Name | Type | Description | Default |
| --- | --- | --- | --- |
| `type` | `string` | HTML input type; passed through to the underlying `<input>`. | — |
| `className` | `string` | Extra Tailwind classes appended to the base styling. | — |
| `…props` | `React.ComponentProps<'input'>` | All other native input attributes and event handlers. | — |

## Usage Notes
- Tailwind selectors already handle disabled opacity and focus rings; only override if introducing new states.
- Pair with the `Label` component for accessible form groupings.
