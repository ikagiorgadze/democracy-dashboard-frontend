# utils (`src/lib/utils.ts`)

## Purpose
- Collects small cross-cutting helpers for class name merging and variable code display names.

## API
- `cn(...inputs: ClassValue[])` → `string` – tailwind-aware class merger using `clsx` + `tailwind-merge`.
- `getDisplayName(codeWithPrefix: string)` → `string` – resolves readable labels for V-Dem and IMF codes, accepting either `DATASET:CODE` or raw `CODE`.

## Usage Notes
- Prefer importing `cn` from this module rather than `clsx`/`twMerge` individually to keep bundle size optimized.
- `getDisplayName` falls back to returning the raw code when no mapping is found; surface TODOs in calling code if a variable unexpectedly lacks a description.
