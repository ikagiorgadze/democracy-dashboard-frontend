# button-variants (`src/components/ui/button-variants.ts`)

## Purpose
- Centralizes Tailwind class combinations for the shared `<Button />` component using `class-variance-authority`.

## API
- `buttonVariants(props?: { variant?: 'default' \| 'destructive' \| 'outline' \| 'secondary' \| 'ghost' \| 'link'; size?: 'default' \| 'sm' \| 'lg' \| 'icon'; className?: string })` → `string`

## Usage Notes
- Additional variants/sizes should be declared here so they are immediately available through the `Button` component’s props.
- Keep SVG sizing rules (`[_svg]:size-4`) in sync with icon usage elsewhere; adjust here if icon footprints change globally.
