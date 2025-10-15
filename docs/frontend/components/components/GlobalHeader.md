# GlobalHeader (`src/components/GlobalHeader.tsx`)

## Purpose
- Renders the persistent top navigation bar with product branding, dataset shortcuts, and a CTA that drops the user into the chart explorer.
- Handles responsive UX by collapsing the action buttons into a Radix dialog sheet on mobile viewports.
- Keeps query-change plumbing available so the header can participate in future global search or filters.

## Key Interactions
- Uses `useNavigate` from React Router to drive route changes (`/`, `/chart`, `/info/v-dem`, `/info/imf`).
- Wraps the mobile menu in `@radix-ui/react-dialog` to provide focus trapping and accessible dismissal.
- Invokes a `goToChart` helper that preserves the current variable selection when deep-linking to `/chart`.

## Props
| Name | Type | Description | Default |
| --- | --- | --- | --- |
| `currentQuery` | `QueryState` | The full query/filter state reflected in the rest of the dashboard. Currently unused but available for future header-driven filters. | — |
| `onQueryChange` | `(query: QueryState) => void` | Callback for mutating query state from header-scope widgets. Reserved for future enhancements. | — |

## Usage Notes
- The logo button always pushes the root route; wrap it in a `<Link>` if you need prefetching.
- Mobile and desktop buttons share the same navigation helpers, so updates must touch both button groups.
- If the header starts mutating query state again, make sure to call `onQueryChange` before navigating to keep URL state in sync.
