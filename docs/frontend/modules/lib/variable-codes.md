# variable-codes (`src/lib/variable-codes.ts`)

## Purpose
- Bridges human-friendly V-Dem variable names to API codes and back, while also incorporating IMF code lookups.
- Provides flexible helpers that recognize both legacy label strings and direct code inputs.

## API
- `VARIABLE_NAME_TO_CODE`, `VARIABLE_CODE_TO_NAME` – merged dictionaries combining curated mappings, translation imports, and manual overrides.
- `getVariableCode(name: string)` → `string | undefined`
- `getVariableName(code: string)` → `string | undefined`
- `getVariableDisplayName(code: string)` → `string`

## Usage Notes
- `getVariableCode` treats inputs starting with `v` or `e_` as already-coded identifiers; callers can pass either plain labels or codes.
- IMF descriptions are folded in via `IMF_WEO_CODE_TO_DESC` and `IMF_NEA_CODE_TO_DESC`, allowing mixed datasets to resolve display names consistently.
- TODO: Audit the manual overrides to ensure de-duplicated entries stay aligned with the backend taxonomy once an authoritative code list is available.
