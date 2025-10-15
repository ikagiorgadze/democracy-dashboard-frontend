# url-state (`src/lib/url-state.ts`)

## Purpose
- Defines the canonical `QueryState` interface for the dashboard and utilities that sync it to/from URL search parameters.

## API
- `DEFAULT_STATE`: baseline values for newly initialized sessions.
- `stateToUrlParams(state: QueryState)` → `URLSearchParams`
- `urlParamsToState(params: URLSearchParams)` → `QueryState`
- `buildChartUrl(baseState, variable, overrides?)` → `string`

## Usage Notes
- New query fields must be added to both serializers to keep deep links accurate; missing entries silently fallback to defaults.
- The serializer limits multi-variable payloads to the first five entries when constructing `vars` to keep URLs manageable.
- TODO: Document the JSON encoding schema for `correlationPairs` and `customPairs` in backend docs so other clients interpret the params consistently.
