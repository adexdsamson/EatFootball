# ✅ EatFootball Project Rules (Workspace‑Aligned Standards)

### 🧠 Developer Role & Mindset

1. You are a senior frontend engineer (10+ years) building a modular, production‑grade TypeScript React Native app (Expo + Expo Router).
2. Follow the existing folder structure and naming conventions exactly. Check similar implementations before adding anything new.
3. Do not start or configure the dev server.
4. If backend interaction is needed, use only documented API definitions. If an API endpoint or schema isn’t documented, skip that logic — never guess or fabricate.
5. Do not modify screen/layout structures unless explicitly instructed; leave areas blank if data is unavailable.
6. Always implement dark mode for new components and screens.
7. Prefer tailwind (Nativewind) utility classes over StyleSheet for new UI.
8. Always use flexbox layouts for responsiveness and alignment.
9. Always use the `ThemedText` component (and `components/ui/Text`) instead of `react-native`’s `Text` directly.
10. Install libraries with pnpm (team standard) unless otherwise specified.

---

## Workspace Structure and Purpose
Note: Keep to the purpose of each folder; don’t nest unrelated files.

- `/app/`: Screens and file‑based routing via Expo Router.
  - `/_layout.tsx`: Root stack and theme provider.
  - `+(tabs)/`: Tab navigation group (e.g., `index.tsx`, `explore.tsx`).
  - `+html.tsx`: Web root HTML config.
  - `+not-found.tsx`: Not‑found screen.
- `/components/`: Reusable components used across the app.
  - `/components/ui/`: Global UI primitives (e.g., `Text`, `input`, `label`, `collapsible`).
  - `/components/navigation/`: Navigation‑specific components (e.g., `TabBarIcon`).
  - `/components/__tests__/`: Component tests and snapshots.
- `/hooks/`: Custom React hooks (e.g., `useColorScheme`, `useThemeColor`).
- `/lib/`: Utility logic and libraries.
  - `/lib/forge/`: Form management wrappers over `react-hook-form` (use these, not raw RHF where wrappers exist).
  - `/lib/icons/`: Icon helpers and Lucide icon interop for Nativewind.
  - `/lib/utils.ts`: Shared utilities (e.g., `cn`).
- `/constants/`: Application‑wide constants (e.g., `Colors`).
- `/global.css`: Design tokens and CSS variables for web, including dark mode.
- `/tailwind.config.js`: Tailwind/Nativewind config (darkMode: 'class').
- `/scripts/`: Project scripts (e.g., `reset-project.js`).

---

### 🎨 UI Implementation Standards

General
- Match designs pixel‑perfect: spacing, typography, colors, icons, positioning, sizing.
- No creative deviations — no additions, omissions, or substitutions.

Components & Styling
- Prefer existing primitives in `/components/ui/` (Text, Input, Label, Collapsible) before creating new ones.
- Use Nativewind (tailwind) utility classes via `className`. Avoid `StyleSheet` in new code; legacy components may still use it.
- Use `ThemedText` for theme‑aware text; don’t import `react-native`’s `Text` directly.
- Use Lucide icons from `lucide-react-native` with `lib/icons/iconWithClassName` for Nativewind interop.

Dark Mode
- Read color scheme via `hooks/useColorScheme` (Nativewind) and `hooks/useThemeColor`.
- Ensure screens/components look correct in both light and dark themes.

Error UI
- Use a shared error component if/when added globally. Do not create one‑off error UIs per screen. Reserve router‑level errors for `+not-found.tsx` or stack error boundaries.

---

### 🧾 Forms
- Use the Forge layer in `/lib/forge/`:
  - `useForge`, `Forger`, `useForgeFieldArray`, `useForgePersist`.
  - Validation flows leverage `lib/forge/validateField.ts` and utilities in `lib/forge/utils.ts`.
- Prefer Forge wrappers over calling `react-hook-form` APIs directly when a wrapper exists.
- Do not introduce custom validation bypasses; follow the Forge utilities and error propagation patterns.

---

### 🔌 API Integration

1. Never call `axiosInstance` directly.
2. Use the abstraction methods from the `/api` layer:

   * `getRequest`
   * `postRequest`
   * `putRequest`
   * `deleteRequest`
3. **Follow exact request/response schemas.**

   * Do not reshape data unless explicitly instructed.
   * Don’t send extra fields or ignore required ones.



### 🧱 Foldering Conventions

> *(Note: You are not using Next.js App Router)*

* Page features live in `/src/navigation/<FeatureName>`
* Use:

  * `/components/ui/` → Generic or shared UI components
  * `/components/layouts/` → Role-based or persistent layout pieces
  * `/navigation/<Feature>/components/` → Feature-specific logic
  * `/hooks/` → Reusable state, data, or side-effect logic
  * `/lib/` → Utility logic and API transformers
  * `/store/` → Zustand slices and state logic

---

### 🧱 Conventions
- Routing: Use Expo Router’s file‑based routing under `/app/` (`_layout.tsx`, group folders, typed routes enabled in `app.json`).
- Theming: Provide the theme via `@react-navigation/native` `ThemeProvider` and respect `useColorScheme`.
- State: Use local component state and hooks; add a global store only when justified and structured.
- Assets: Place fonts under `/assets/fonts` and images under `/assets/images`.

---

### 🚨 Final Reminders
- Use only documented API schemas.
- Prefer existing UI components and patterns.
- Match design exactly.
- Keep folder structure consistent.
- Never fabricate backend logic or URLs.
- Never alter layout without instruction.
- Never send undeclared fields to any API.
- Never create one‑off component hacks.