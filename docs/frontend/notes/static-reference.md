# Static Reference Build – `npm run docs:build`
- Command: `npm run docs:build`
- Outcome: ❌ Failed during `typedoc` phase.
- Artifacts: `docs/typedoc` missing; `docs/props.json` skipped because the chain aborted before `npm run docs:props`.
- Notable warning: glob `/src/index.tsx` missing (Typedoc config expects file that does not exist).
- Blocking error: `src/pages/ChartExplorer.tsx:257` – TS2345 (`readonly [string, VDemDataPoint[]]` not assignable to mutable tuple). Requires code fix or overload adaptation before static docs can compile.
- Next step: decide whether to adjust the reducer utilities to avoid returning `readonly` tuples or update Typedoc config; outside this documentation pass's scope.
