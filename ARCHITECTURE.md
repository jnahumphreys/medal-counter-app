# Medal Counter App — Architecture and Implementation Plan

## Objective

Build a production-ready Olympic Medal Counter app using React and TypeScript.  
The app displays the top 10 countries sorted by medal type, controlled by a `?sort=` URL parameter or by user interaction.  
The architecture emphasizes:
- Separation of concerns
- Single source of truth (state)
- Pure, declarative presentational components

---

## Technologies and Libraries

- React + Hooks — UI framework
- TypeScript — type safety
- Vite — fast build & development
- Zustand — lightweight global state management
- TailwindCSS — utility-first styling
- ESLint + Prettier — linting and formatting
- Storybook — UI development & documentation
- Cypress — end-to-end testing
- DevContainers — containerized development environments
- GitHub Actions — automated workflows
- Husky — pre-commit hooks

---

## Application Layers & Patterns

### State Management

Global state is managed via Zustand, with the following shape:
```ts
interface MedalStore {
  medals: MedalEntry[];
  sortKey: 'gold' | 'silver' | 'bronze' | 'total';
  error: string | null;

  setMedals(medals: MedalEntry[]): void;
  setError(message: string): void;

  sortByGold(): void;
  sortBySilver(): void;
  sortByBronze(): void;
  sortByTotal(): void;
}
```

The store exposes domain-specific actions (`sortByGold`, etc.) instead of generic `setSortKey` to keep the UI declarative and domain-agnostic.

### Derived State

- Sorting is implemented as a pure utility: `sortMedals()`.
- `useSortedMedals()` hook subscribes to `medals` and `sortKey` and returns a memoized, sorted list.

### Initialization & Data Fetch

- App initialization happens *outside* the React tree in `initApp()`.
- On startup:
  - Reads & validates the `?sort=` URL param.
  - Defaults to `'gold'` if invalid or missing.
  - Seeds `sortKey` into the store.
  - Fetches `medals.json` and populates the store.
  - Sets an error in store if fetch fails.

---

## Data Flow

1. `main.tsx` calls `initApp()` before rendering React.
2. `initApp()` reads the URL param, fetches data, and seeds the store.
3. `medals` and `sortKey` live in Zustand as single source of truth.
4. Components subscribe to store slices and render declaratively.
5. User interactions (clicking sort buttons) trigger store actions to update `sortKey`, recomputing derived data.

---

## Data Schema

### Medal Entry
```ts
interface MedalEntry {
  code: string;  // ISO country code, e.g., "USA"
  gold: number;
  silver: number;
  bronze: number;
}
```

### Example `medals.json` entry:
```json
{
  "code": "USA",
  "gold": 9,
  "silver": 7,
  "bronze": 12
}
```

---

## URL Parameter

- Supports: `?sort=gold | silver | bronze | total`
- Defaults to `'gold'` if invalid or missing.
- On sort change, the URL is updated with `history.replaceState` for shareability.

---

## Folder Structure

```
src/
  App.tsx
  main.tsx
  initApp.ts

  components/
    AppTitle.tsx
    MedalTableHeader.tsx
    MedalTableBody.tsx
    EntrantRow.tsx
    Flag.tsx
    ErrorFeedback.tsx
    SortByGoldButton.tsx
    SortBySilverButton.tsx
    SortByBronzeButton.tsx
    SortByTotalButton.tsx
    common/
      SortButton.tsx

  store/
    useMedalStore.ts

  hooks/
    useSortedMedals.ts

  utils/
    sortMedals.ts
```

---

## Component & File Responsibilities

### Application Shell

#### `main.tsx`
- Entry point
- Calls `initApp()`
- Mounts `<App />` into the DOM

#### `App.tsx`
- Root React component tree
- Composes UI layout
- Renders child components

#### `initApp.ts`
- Reads & validates URL param
- Fetches `medals.json`
- Seeds store with `medals`, `sortKey`, and errors (if any)

---

### Presentational Components

#### `components/AppTitle.tsx`
- Renders application title

#### `components/MedalTableHeader.tsx`
- Renders `<thead>` with 4 `SortByXButton` components

#### `components/MedalTableBody.tsx`
- Renders `<tbody>` with sorted rows
- Uses `useSortedMedals()`

#### `components/EntrantRow.tsx`
- Renders a single entrant’s row with flag and medals

#### `components/Flag.tsx`
- Renders country flag based on `code` prop

#### `components/ErrorFeedback.tsx`
- Displays error banner if `store.error` is set
- Includes reload button

---

### Sort Buttons

#### `components/SortByGoldButton.tsx`
#### `components/SortBySilverButton.tsx`
#### `components/SortByBronzeButton.tsx`
#### `components/SortByTotalButton.tsx`
- Domain-aware wrappers around `SortButton`
- Subscribe to `sortKey`
- Call appropriate `store.sortByX()` action
- Pass props to `SortButton`

#### `components/common/SortButton.tsx`
- Pure, reusable presentational button
- Accepts `sortKey`, `active`, `onClick` props
- Maps `sortKey` to label and color internally

---

### Business Logic

#### `store/useMedalStore.ts`
- Holds `medals`, `sortKey`, and `error`
- Provides actions:
  - `setMedals()`, `setError()`
  - `sortByGold()`, `sortBySilver()`, etc.

#### `hooks/useSortedMedals.ts`
- Derived state
- Uses `medals` + `sortKey` to return sorted data

#### `utils/sortMedals.ts`
- Pure sorting utility
- Accepts `medals` + `sortKey` and returns sorted array

---

## Store Actions

The store exposes domain-specific actions to keep the UI declarative:
```ts
sortByGold: () => set({ sortKey: 'gold' }),
sortBySilver: () => set({ sortKey: 'silver' }),
sortByBronze: () => set({ sortKey: 'bronze' }),
sortByTotal: () => set({ sortKey: 'total' })
```

These:
- Encapsulate domain logic in one place
- Avoid hardcoding strings in UI
- Allow future enhancements (analytics, validation, etc.)

---

## Notes on Patterns

- Business logic (URL parsing, data fetch, sorting rules) lives outside React.
- Zustand is the single source of truth.
- React components are declarative and presentational only.
- Sorting logic is isolated in `sortMedals()` for testability.
- Derived state encapsulated in selector hook.

---

## Testing

Testing will be implemented across three layers:

### 1. Unit Testing (with Jest)
- Pure logic functions like `sortMedals()` will be covered with unit tests.
- Edge cases such as tie-breaking and empty arrays will be validated.

### 2. Component Testing (with Storybook Test Runner)
- Pure presentational components will be tested in isolation using Storybook’s test runner.
- Snapshot tests, interaction tests, and accessibility checks will ensure UI correctness.
- Stories serve both documentation and test surface.

### 3. End-to-End Testing (with Cypress)
- Full user journeys will be tested via Cypress.
- Ensures data flow from store → components → UI behaves as expected.
- Covers interactions (e.g. clicking sort buttons), error states, and URL param parsing.

---

## Rationale

This project makes intentional, opinionated choices to support maintainability, performance, and developer clarity. Below are the core decisions and tradeoffs:

---

### State Management: Why Zustand?

- **Minimal boilerplate** compared to `useReducer` + Context or Redux.
- **Fine-grained subscriptions** reduce unnecessary re-renders.
- **Encourages separation of concerns** — store lives outside the React tree.
- Domain-specific actions like `sortByGold()` keep business logic abstracted from the UI.
- Zustand scales well without introducing complexity or opinionated structure.
- Redux and MobX are more powerful, but overkill for this domain with added complexity.

---

### Routing: Why native URL API over React Router?

- The app uses a **single `?sort=` param** — no pages or nested routing.
- Avoids pulling in the full Router dependency and context setup.
- Keeps routing logic **explicit and tightly scoped** to initialization and state syncing.
- Native APIs like `URLSearchParams` and `history.replaceState` are sufficient and stable.

---

### App Framework: Why Vite instead of Next.js?

- No SSR, dynamic routing, or API layer required — **Next.js adds complexity** we don’t need.
- Vite offers:
  - **Faster dev server startup**
  - **Hot module reload**
  - **Simpler config**
- Ideal for fast single-page-app prototyping and production delivery.

---

### Component Architecture

- **Business logic lives outside of React**, preserving declarative rendering in components.
- Components are **pure and presentational**, with props only — no internal state or side effects.
- **Derived state is computed via hooks** like `useSortedMedals()` and utilities like `sortMedals()`.
- **Explicit, domain-specific actions** (`sortByGold`, etc.) avoid passing string literals or keys throughout the UI.
- Results in **testable**, **composable**, and **readable** component logic.

---

### Why Storybook?

- Enables **isolated development** and documentation of UI components.
- Supports **visual testing, accessibility checks, and interaction testing**.
- Facilitates team collaboration and stakeholder review without launching the app.
- Encourages **component-driven architecture** and reuse.

---

### Summary of Design Principles

- 🧠 **Single source of truth**: Zustand holds the entire app state.
- 🎯 **Domain-driven actions**: UI issues intents, store handles the logic.
- 📦 **Separation of concerns**: data, logic, and view layers are clearly partitioned.
- 🔍 **Explicit flows**: No magic, everything traceable and testable.
- 🔧 **Lean tooling**: All libraries selected for low setup and high clarity.

These decisions result in an architecture that’s fast to build, easy to reason about, and ready for extension.

---
