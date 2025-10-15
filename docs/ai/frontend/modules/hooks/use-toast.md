# use-toast (`src/hooks/use-toast.ts`)

## Purpose
- Client-side toast store modeled after shadcn’s example, customized to enforce a single active toast and expose dismiss/update helpers.

## API
- `useToast()` → `{ toasts: ToastProps[]; toast: (opts: ToastOpts) => { id: string; dismiss(): void; update(next: ToastProps): void }; dismiss(toastId?: string): void }`
- `toast(opts: ToastOpts)` – convenience export that enqueues a toast without manually calling the hook.
- `reducer(state, action)` – exposed for testing; handles `ADD_TOAST`, `UPDATE_TOAST`, `DISMISS_TOAST`, and `REMOVE_TOAST`.

## Usage Notes
- `TOAST_LIMIT` is set to `1`, meaning new toasts replace older ones; adjust if the UX should allow stacking.
- `TOAST_REMOVE_DELAY` is intentionally large (≈16.6 minutes) so toasts stay visible until dismissed; lower this value if automatic clearance is desired.
- TODO: If toasts need persistence across tabs, swap the in-memory `listeners` array with a context provider or external state container.
