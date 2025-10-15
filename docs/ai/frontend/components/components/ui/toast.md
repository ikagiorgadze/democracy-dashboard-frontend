# toast (`src/components/ui/toast.tsx`)

## Purpose
- Exposes styled wrappers around Radix Toast primitives plus TypeScript helpers used by the custom toast store.

## Key Interactions
- Defines a shared `ToastProvider`, `ToastViewport`, `Toast`, `ToastTitle`, `ToastDescription`, `ToastClose`, and `ToastAction` with shadcn-tailwind classnames.
- Applies `cva` variants so destructive toasts automatically pick up red theming.
- Re-exports `ToastProps` and `ToastActionElement` type aliases consumed in `use-toast.ts`.

## Props
- `Toast` accepts all Radix toast props plus a `variant` (`default` or `destructive`).
- `ToastAction`/`ToastClose`/`ToastViewport` mirror their Radix counterparts while adding Tailwind classes.

## Usage Notes
- `ToastClose` sets `toast-close` attributes expected by shadcn styles; keep that attribute when customizing.
- `ToastAction` already handles destructive grouping, so wrap your action button content directly without extra styling.
