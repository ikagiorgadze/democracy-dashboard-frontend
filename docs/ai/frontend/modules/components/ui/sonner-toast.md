# sonner-toast (`src/components/ui/sonner-toast.ts`)

## Purpose
- Thin re-export of `toast` from the `sonner` package so the rest of the codebase can import from the local UI namespace.

## API
- `toast` – identical to `sonner`’s `toast` function; see upstream docs for available signatures.

## Usage Notes
- Use this re-export instead of importing directly from `sonner` to keep the dependency surface centralized (useful if the library is swapped later).
