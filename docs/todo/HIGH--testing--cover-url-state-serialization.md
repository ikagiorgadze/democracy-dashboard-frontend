---
id: test-url-state
title: "Cover URL state serialisation"
severity: HIGH
type: testing
component: "src/lib/url-state.ts"
status: open
estimate: M
dependencies: ["harden-url-state"]
---

## Rationale
`QueryState` drives every page, yet there are no tests guaranteeing `stateToUrlParams` and `urlParamsToState` stay in sync. Given the MVP’s reliance on shareable links (docs/frontend/routing.md), missing coverage makes regressions easy when expanding query fields.

## Evidence
- Absence of any `*.test.ts` files (`find src -name '*test*'`).
- Critical logic at `src/lib/url-state.ts:37`-`src/lib/url-state.ts:131` converts state to and from URLs without automated verification.

## Impact
Future changes (new filters, validation) can silently break deep links, trapping users on stale charts or throwing runtime errors. Without regression tests, maintainers must manually verify every parameter permutation.

## Proposed Change
Add unit tests that exercise round-trip serialization, default fallbacks, and edge cases (empty arrays, mixed correlation data). Use table-driven tests to cover both regular and malformed inputs once validation is in place.

## Acceptance Criteria
- [ ] `stateToUrlParams` and `urlParamsToState` have tests covering baseline, multi-variable, and correlation scenarios.
- [ ] Tests verify URL encoding/decoding of category/subcategory slugs.
- [ ] Malformed JSON inputs for `corr-pairs`/`custom-pairs` are handled as expected (after validation work).
- [ ] Round-trip tests confirm no unintended data loss.

## Tasks
- [ ] Set up a test runner (shared with broader suite) for lib modules.
- [ ] Write table-driven test cases for serialization/deserialization.
- [ ] Add negative tests for malformed values (pending validation implementation).
- [ ] Document test strategy in docs/frontend/state.md or README.

## Rollout & Risk
Low risk; isolated unit tests. Coordinate with URL validation refactor to avoid churn. Backout requires removing the new tests if they block CI temporarily.

## References
- docs/frontend/routing.md
- src/lib/url-state.ts
