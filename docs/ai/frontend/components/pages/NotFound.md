# NotFound (`src/pages/NotFound.tsx`)

## Purpose
- Default router fallback that logs 404 attempts and offers a link back to the homepage.

## Key Interactions
- Calls `useLocation()` to capture the unmatched path and logs it via `console.error` during mount.
- Provides a semantic 404 layout with minimal Tailwind styling.

## Usage Notes
- Consider replacing the raw anchor with `Link` from React Router if client-side navigation should avoid full reloads.
