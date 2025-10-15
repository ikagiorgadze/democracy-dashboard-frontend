---
id: test-data-transform
title: "Test API data transformations"
severity: MEDIUM
type: testing
component: "src/lib/data.ts"
status: open
estimate: M
dependencies: ["stop-fake-data"]
---

## Rationale
`transformApiData` normalises backend results, matches country names, and coerces values, but none of these code paths are verified. As we remove synthetic fallbacks and rely on live data (docs/frontend/state.md), we need regression tests to ensure mappings stay stable.

## Evidence
- `src/lib/data.ts:14`-`src/lib/data.ts:92` performs multiple string-normalisation passes, ISO matching, and value coercion without tests.
- `find src -name '*test*'` returns nothing, confirming no existing coverage.

## Impact
Changes to country metadata or API payloads could silently drop series (when name matching fails) or return `NaN`. Without tests, such regressions only surface in production charts, undermining data integrity.

## Proposed Change
Add unit tests that feed representative API payloads (including diacritics, ISO fallbacks, BigInt years) through `transformApiData`/`fetchVDemData` with mocked services. Verify that unmatched countries are skipped and values stay numeric after coercion.

## Acceptance Criteria
- [ ] Tests cover direct name matches, substring matches, and ISO code fallback.
- [ ] BigInt `year` values are converted to numbers as expected.
- [ ] Null or undefined metric values are excluded from results.
- [ ] When codes are unknown, the functions respond according to the updated reliability policy (no synthetic data).

## Tasks
- [ ] Mock `apiService` responses in tests to isolate transformation logic.
- [ ] Craft fixtures representing tricky country-name variants and BigInt payloads.
- [ ] Assert on returned `VDemDataPoint[]` contents and ordering.
- [ ] Update docs/frontend/modules/lib/data.md with testing notes.

## Rollout & Risk
Pure unit tests; risk is low. Ensure they integrate with the broader test harness added in `add-foundational-tests`. Backout simply removes or skips the new tests.

## References
- docs/frontend/state.md
- src/lib/data.ts
- src/lib/api.ts
