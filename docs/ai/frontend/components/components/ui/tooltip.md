# tooltip (`src/components/ui/tooltip.tsx`)

## Purpose
- Wraps Radix Tooltip primitives with shared Tailwind styling for content popovers throughout the app.

## Key Interactions
- Re-exports `TooltipProvider`, `Tooltip`, `TooltipTrigger`, and `TooltipContent`; only `TooltipContent` customizes styling.
- Sets a default `sideOffset` of 4px and animates entry/exit using shadcn motion classes.

## Usage Notes
- Wrap the entire dashboard in a single `TooltipProvider` (already done in `App.tsx`) to enable pointer delay options if needed.
- The provider can accept a `delayDuration` prop; pass it at the usage site when hovering tooltips should open faster or slower.
