# sonner (`src/components/ui/sonner.tsx`)

## Purpose
- Configures the third-party `sonner` toaster instance with theme-aware styling to match the UI when the app switches themes.

## Key Interactions
- Pulls the active theme from `next-themes` (set up in the broader app shell) and threads it into the `Sonner` component.
- Applies class overrides for toast shell, description, action, and cancel buttons via the `toastOptions` prop.

## Props
- Accepts all props supported by `sonner`’s `Toaster` component; they are forwarded through the spread operator.

## Usage Notes
- Ensure `ThemeProvider` from `next-themes` wraps the app; otherwise `useTheme` will fall back to `"system"`.
- This toaster is rendered alongside the Radix-based `<Toaster />`; both can coexist because they drive different toast systems (`sonner` vs custom).
