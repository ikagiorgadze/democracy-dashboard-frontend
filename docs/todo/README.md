Audit date (UTC): 2025-10-15 16:32:38 UTC

## Issue Counts
- Severity — BLOCKER: 1, HIGH: 4, MEDIUM: 4, LOW: 1
- Type — reliability: 2, architecture: 2, testing: 4, dx: 1

| id | title | severity | type | component | status | estimate |
| --- | --- | --- | --- | --- | --- | --- |
| stop-fake-data | Remove synthetic data fallback on API errors | BLOCKER | reliability | src/lib/data.ts | open | M |
| harden-url-state | Validate URL query state parsing | HIGH | reliability | src/lib/url-state.ts | open | M |
| split-chart-explorer | Modularize ChartExplorer responsibilities | HIGH | architecture | src/pages/ChartExplorer.tsx | open | L |
| add-foundational-tests | Add foundational automated test suite | HIGH | testing | repo-wide | open | L |
| test-url-state | Cover URL state serialisation | HIGH | testing | src/lib/url-state.ts | open | M |
| react-query-chart-data | Migrate chart data fetching to React Query | MEDIUM | architecture | src/pages/ChartExplorer.tsx | open | L |
| validate-config | Validate runtime API configuration | MEDIUM | architecture | src/lib/api.ts | open | S |
| test-data-transform | Test API data transformations | MEDIUM | testing | src/lib/data.ts | open | M |
| test-chart-explorer | Add ChartExplorer interaction tests | MEDIUM | testing | src/pages/ChartExplorer.tsx | open | L |
| gate-debug-logs | Gate debug logging behind environment checks | LOW | dx | src/pages/ChartExplorer.tsx | open | S |

## Getting Started
- Resolve the BLOCKER first to restore trustworthy data handling.
- Address HIGH severity issues next to stabilise routing and reduce structural risk.
- Tackle MEDIUM architecture improvements, then clean up DX items once core flows are solid.
