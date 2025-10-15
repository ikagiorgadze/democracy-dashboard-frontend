# help-icon (`src/components/ui/help-icon.tsx`)

## Purpose
- Simple wrapper around Lucide's `HelpCircle` icon that ensures consistent sizing and muted coloring across tooltips and contextual help affordances.

## Key Interactions
- Accepts arbitrary span props (including `aria-label`) and merges them with default sizing classes.

## Props
| Name | Type | Description | Default |
| --- | --- | --- | --- |
| `className` | `string` | Tailwind classes applied to the outer span for custom sizing or spacing. | `"h-5 w-5"` |
| `aria-label` | `string` | Accessible label when the icon is used as a standalone control. | — |
| `…rest` | `React.HTMLAttributes<HTMLSpanElement>` | Any additional span attributes (e.g., `role`). | — |

## Usage Notes
- Use alongside `TooltipTrigger` to provide textual descriptions; pass `aria-hidden="true"` when nested inside a button with labelled text.
