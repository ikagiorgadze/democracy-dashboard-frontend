# select (`src/components/ui/select.tsx`)

## Purpose
- Provides a full Radix Select implementation with shadcn-aligned theming for trigger, content, items, and scroll buttons.

## Key Interactions
- Re-exports Radix primitives (`Select`, `SelectGroup`, `SelectValue`) alongside styled wrappers (`SelectTrigger`, `SelectContent`, etc.).
- Configures `position="popper"` behavior by default and ensures the viewport width tracks the trigger width.

## Props
- Each export mirrors its Radix counterpart while merging Tailwind classes. Refer to Radix docs for supported props.

## Usage Notes
- When using `SelectContent`, pass `position="item-aligned"` if the dropdown should not match trigger width.
- `SelectItem` inserts a `SelectPrimitive.ItemIndicator` with a `Check` icon; avoid nesting custom icons inside the item.
