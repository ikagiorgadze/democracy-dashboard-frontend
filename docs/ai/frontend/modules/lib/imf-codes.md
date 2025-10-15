# imf-codes (`src/lib/imf-codes.ts`)

## Purpose
- Houses the extensive mapping between IMF WEO/NEA indicator codes and their descriptions, along with helpers for reverse lookup and code detection.

## API
- `IMF_WEO_CODE_TO_DESC`, `IMF_NEA_CODE_TO_DESC` – `Record<string, string>`
- Reverse maps: `IMF_WEO_DESC_TO_CODE`, `IMF_NEA_DESC_TO_CODE`
- `IMF_CODE_PATTERN` – Regex used to detect IMF-formatted codes.
- `getImfVariableCode(nameOrCode)` → `string | undefined`

## Usage Notes
- `getImfVariableCode` first checks the formatting regex, then searches description maps; ensure new dataset descriptions match exactly to resolve properly.
- Consider offloading the large mapping objects to JSON imports if bundle size becomes a concern, though current Vite tree-shaking keeps them manageable.
