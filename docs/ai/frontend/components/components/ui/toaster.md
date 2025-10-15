# toaster (`src/components/ui/toaster.tsx`)

## Purpose
- Portal component that renders queued toasts from the custom `useToast` hook using Radix Toast primitives.

## Key Interactions
- Pulls toast entries from `useToast()` and maps them into `<Toast>` instances with optional action buttons.
- Keeps `ToastProvider` and `ToastViewport` colocated so callers can drop `<Toaster />` at the root of the app.

## Props
- This component does not accept props; it consumes global toast state from the context exposed by `useToast`.

## Usage Notes
- Include exactly one `<Toaster />` in the app tree (currently placed inside `App.tsx`) to avoid duplicated queues.
- The hook enforces a single-toast limit (`TOAST_LIMIT = 1`); adjust the constant in `use-toast.ts` if multiple concurrent toasts are required.
