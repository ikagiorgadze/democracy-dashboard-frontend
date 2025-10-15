# main (`src/main.tsx`)

## Purpose
- Vite entry point that mounts the React application into the DOM.

## Key Interactions
- Imports global Tailwind styles (`index.css`) and renders `<App />` into the `#root` element using the modern `createRoot` API.

## Usage Notes
- Ensure `index.html` continues to expose a matching `id="root"` container; any hydration features should be implemented here before calling `render`.
