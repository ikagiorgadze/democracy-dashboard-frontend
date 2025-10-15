---
id: stop-fake-data
title: "Remove synthetic data fallback on API errors"
severity: BLOCKER
type: reliability
component: "src/lib/data.ts"
status: open
estimate: M
dependencies: []
---

## Rationale
Serving fabricated metrics whenever upstream APIs error makes the dashboard misleading and violates the documentation promise that charts reflect real V-Dem/IMF data (see docs/frontend/overview.md). The current fallback masks backend regressions and removes any signal that data quality degraded.

## Evidence
`src/lib/data.ts:94`-`src/lib/data.ts:139`
```ts
// Sample data generator for demo purposes (fallback)
function generateSampleData(...) {
  const randomVariance = (Math.random() - 0.5) * config.variance;
  ...
}
```
`src/lib/data.ts:186`-`src/lib/data.ts:205`
```ts
  } catch (error) {
    console.error('API call failed, falling back to sample data:', error);
    return generateSampleData(...);
  }
```

## Impact
Users silently receive random values, eroding trust and potentially leading to incorrect analysis whenever the backend is unavailable or data mappings fail. Operationally the frontend never alerts engineers that an upstream outage occurred, prolonging downtime.

## Proposed Change
Propagate API failures up to the UI instead of fabricating data. Surface an error state (toast plus inline chart message) and add observability so we can detect repeated failures. Retain optional feature-flagged demo data only in explicitly opt-in development modes.

## Acceptance Criteria
- [ ] `fetchVDemData` throws or returns an error result when the API call fails.
- [ ] UI displays a clear error and does not render random data when upstream responses are missing.
- [ ] Monitoring/logging captures the failure path for visibility.
- [ ] Optional demo-mode fallback is guarded behind a development-only flag.

## Tasks
- [ ] Refactor `fetchVDemData` to remove the unconditional `generateSampleData` fallback.
- [ ] Update consuming components to handle and display error states.
- [ ] Add telemetry or structured logging for the failure branch.
- [ ] Document demo-mode behavior in docs/frontend if we keep it for local development.

## Rollout & Risk
Coordinate with backend ops so removing the fallback does not produce blank charts in production without messaging. Roll out behind a feature flag if needed, monitor API error rates, and be ready to revert by re-enabling the guard if user impact is observed.

## References
- docs/frontend/overview.md
- src/lib/data.ts
