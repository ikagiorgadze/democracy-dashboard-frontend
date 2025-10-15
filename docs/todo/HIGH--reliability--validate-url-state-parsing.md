---
id: harden-url-state
title: "Validate URL query state parsing"
severity: HIGH
type: reliability
component: "src/lib/url-state.ts"
status: open
estimate: M
dependencies: []
---

## Rationale
Deep links are a core workflow per docs/frontend/routing.md, but `urlParamsToState` trusts unvalidated query strings. Crafted or stale links that contain invalid JSON or out-of-range numbers crash parsing and put `NaN`/`undefined` into state, breaking chart rendering.

## Evidence
`src/lib/url-state.ts:91`-`src/lib/url-state.ts:115`
```ts
startYear: parseInt(params.get('from') || DEFAULT_STATE.startYear.toString()),
...
correlationPairs: params.get('corr-pairs') ?
  JSON.parse(params.get('corr-pairs')!) as CorrelationPair[] :
  DEFAULT_STATE.correlationPairs,
customPairs: params.get('custom-pairs') ?
  JSON.parse(params.get('custom-pairs')!) as Array<{ var1: string; var2: string }> :
  DEFAULT_STATE.customPairs
```
None of these calls guard against `NaN`, `Infinity`, or parsing errors.

## Impact
Any malformed URL (including user typo, truncated share link, or manual tampering) will throw during render or leave the app stuck in an invalid state. This undermines shareable links, hurts reliability, and creates a trivial denial-of-service vector for public embeds.

## Proposed Change
Introduce robust parsing with schema validation (e.g., Zod) that clamps year ranges, validates enum values, and safely handles JSON blobs with try/catch. Unknown or invalid inputs should fall back to defaults while logging for diagnostics.

## Acceptance Criteria
- [ ] URL parsing never throws on invalid input and returns a sanitised `QueryState`.
- [ ] Year values are clamped to allowed ranges and default when missing or invalid.
- [ ] JSON parameters (`corr-pairs`, `custom-pairs`) fall back gracefully when malformed.
- [ ] Automated tests cover representative malformed URLs and confirm safe defaults.

## Tasks
- [ ] Add a parsing helper (e.g., `parseUrlParams`) with schema validation for each field.
- [ ] Update `urlParamsToState` to use the helper and catch JSON parsing errors.
- [ ] Write unit tests for valid and invalid URL examples.
- [ ] Document supported query parameters and validation behavior.

## Rollout & Risk
Changes touch global navigation; verify on staging that existing saved links still work. Monitor logs for validation fallbacks to identify real-world bad URLs. Backout is low risk: revert to previous parsing if unexpected regressions appear.

## References
- docs/frontend/routing.md
- src/lib/url-state.ts
