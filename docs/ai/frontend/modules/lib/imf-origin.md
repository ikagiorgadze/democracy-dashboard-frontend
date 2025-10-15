# imf-origin (`src/lib/imf-origin.ts`)

## Purpose
- Remembers whether a selected IMF indicator originated from the WEO or NEA catalogue so downstream API calls can hit the correct endpoint.

## API
- Type: `ImfOrigin = 'weo' | 'nea'`
- `setImfOrigin(code, origin)` – caches origin metadata for the provided code.
- `getImfOrigin(code)` → `ImfOrigin | undefined`

## Usage Notes
- The map lives in module scope, so it resets on full page reloads; if persistence across sessions is required, promote it to context or localStorage.
