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

Global state is managed via Zustand, composed from feature-specific slices. Example shape:

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

The store exposes domain-specific actions (`sortByGold`, etc.) instead of generic `setSortKey`, this is to:

- Encapsulate domain logic in one place
- Avoid hardcoding strings in UI
- Allow future enhancements (analytics, validation, etc.)

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

```txt
src/
  features/
    entrantsList/
      components/
        EntrantListItem.tsx
        EntrantsList.tsx
        Flag.tsx
      containers/
        EntrantsList.tsx
      logic/
        entrantsSlice.ts
      tests/
        (unit tests, Storybook tests, etc.)
      index.ts (public API, exports nessesary modules)

    sortEntrants/
      components/
        SortEntrants.tsx
        SortByMedal.tsx
        SortByTitle.tsx
      containers/
        SortByGold.tsx
        SortBySilver.tsx
        SortByBronze.tsx
        SortByTotal.tsx
        SortEntrants.tsx
      logic/
        sortSlice.ts
        sortMedals.ts
        useSortedMedals.ts
      tests/
        (unit tests, Storybook tests, etc.)
      index.ts (public API, exports nessesary modules)

    syncSortQueryParam/
      logic/
        parseQueryParam.ts
        updateQueryParam.ts
      tests/
        (unit tests, etc.)
      index.ts (public API, exports nessesary modules)

    errorFeedback/
      components/
        ErrorFeedback.tsx
      containers/
        ErrorFeedback.tsx
      logic/
        errorSlice.ts
      tests/
        (unit tests, Storybook tests, etc.)
      index.ts (public API, exports nessesary modules)

  views/
    main/
      components/
        AppTitle.tsx
        MainView.tsx
      containers/
        MainView.tsx
      tests/
        (unit tests, Storybook tests, etc.)
      index.ts (public API, exports nessesary modules)
      
  store/
    useMedalStore.ts

  types/
    MedalEntry.ts

  styles/
    tailwind.css

  initApp.ts
  App.tsx
  index.tsx
```

---

## Directory Structure Rationale

This project originally followed a flat structure, but was refactored to adopt a **feature-based architecture**. This change was made to reflect how real-world applications scale and how features evolve independently.

### Why the Change?

- As the app grew, it became clear that grouping files by technical type (e.g. `components/`, `store/`, `utils/`) caused friction when working feature-by-feature.
- Instead, a feature-based layout keeps all related logic (state, UI, tests) together, reducing context switching.
- It reflects how the GitHub issues and workstreams are organized — by feature/epic — allowing for atomic PRs and iterative development.

### Benefits of Feature-Based Structure

- **Domain-Driven Separation**  
  Each feature (e.g. viewing entrants, sorting, error handling) has its own folder containing components, logic, and tests. This reflects product requirements and epics directly.

- **Scalable and Maintainable**  
  New features can be added with minimal risk of entanglement. Logic is easier to refactor in isolation.

- **Encapsulation**  
  Business logic is colocated with its UI and tests. No need to jump between folders to understand how a feature works.

- **Improved Traceability**  
  Easy to track changes and map functionality to business requirements.

- **Composable Store**  
  Zustand slices are defined per feature and composed in `shared/store/useMedalStore.ts`, maintaining a unified global state with clear feature ownership.

- **Declarative UI**  
  Business logic like sorting and query param parsing is outside the React tree. Components remain pure and render declaratively.

---

## Component Structure & Naming Convention

To promote clarity and modularity, the application follows a feature-based directory structure. Each feature directory (e.g. `sortEntrants`, `entrantsList`) encapsulates all the related business logic, presentational components, container components, and tests for that domain.

### Presentational vs Container Components

Each feature may define:

- **Presentational Components**: Pure, stateless, and reusable UI components that rely entirely on props. These live in the `components/` subdirectory. They are suitable for isolated rendering in Storybook and do not access application state or side effects directly.

- **Container Components**: Feature-aware components that subscribe to global state (e.g., Zustand) and dispatch actions. These live in the `container/` subdirectory and are responsible for wiring application logic to UI.

This separation ensures that presentation logic remains testable, reusable, and isolated from business logic.

### Naming Convention

We intentionally keep the **same component name** for both the pure and connected versions (e.g. `SortEntrants`) to reflect that they represent the same conceptual UI, just at different levels of abstraction:

- The pure version lives in `components/SortEntrants.tsx`
- The connected version lives in `container/SortEntrants.tsx`
- The public feature entrypoint (`index.tsx`) exports the connected version for use in `App.tsx` and other consumers.

This naming strategy allows consumers to treat the feature as a black box, importing from `features/sortEntrants` without needing to understand its internal layering. It also keeps co-located files naturally aligned and reduces mental overhead when navigating between UI and logic.

By adopting this approach, we preserve separation of concerns while maximizing discoverability and composability within each feature.

---

## Testing Strategy

Testing is performed at multiple layers:

### 1. Unit Testing (with Jest)
- Pure logic functions (e.g. `sortMedals`) are tested in isolation.
- Edge cases like tie-breaking and invalid inputs are covered.

### 2. Component Testing (with Storybook Test Runner)
- Presentational components are tested in isolation.
- Includes snapshot tests, interaction testing, and accessibility checks.

### 3. End-to-End Testing (with Cypress)
- Simulates real user interactions across the full stack.
- Covers navigation, sort selection, error handling, and URL param behavior.

---

## Rationale

This project makes intentional, opinionated choices to support maintainability, performance, and developer clarity.

### Why Zustand?

- Minimal boilerplate compared to useReducer + Context or Redux.
- Fine-grained subscriptions reduce unnecessary re-renders.
- Store lives outside React tree for separation of concerns.
- Domain-specific actions like `sortByGold()` keep logic abstracted.
- Redux and MobX offer more power but add unnecessary complexity for this scope.

### Why Native URL API over React Router?

- Only one query param (`?sort=`), no route nesting required.
- `URLSearchParams` and `history.replaceState` are stable and explicit.
- Avoids extra dependency and context setup.

### Why Vite instead of Next.js?

- No need for SSR, routing, or API routes.
- Vite provides faster builds and simpler config.
- Ideal for single-page app prototyping and deployment.

### Why Storybook?

- Enables isolated UI development and documentation.
- Encourages component reuse and visual regression testing.
- Supports interaction testing and a11y checks.

- ### Feature-Based Epics and Vertical Task Flow

To ensure clarity, testability, and incremental delivery, features are organized as vertical epics in GitHub — each representing a specific domain capability (e.g. sorting entrants, viewing medal data, handling errors).

Each epic contains a linear (waterfall) progression of atomic tasks:

1. Setup any additional dependencies or tooling
2. Write business logic (e.g. Zustand slice, utilities)
3. Compose UI components (with Storybook support)
4. Add unit and interaction tests
5. Add E2E tests (Cypress) if needed
6. Raise PR and release

This structure enables:

- **Iterative release** — Core functionality can ship early, with enhancements layered in later
- **Atomic PRs** — Each task delivers clear value and can be reviewed/tested in isolation
- **Tight alignment with architecture** — Feature folders map 1:1 with epics and their tasks
- **Parallel progress** — UI, logic, and tests can move forward in small units without waiting for an entire feature to be done
- **Low technical debt** — Features are validated end-to-end before moving on

This approach mirrors the structure of the file system and promotes maintainability as the app scales.

---

## Summary of Principles

- 🧠 Single source of truth via Zustand
- 🔧 Business logic lives outside the React tree
- 🎯 Domain-specific actions avoid leaking implementation into UI
- 🧱 Feature-based structure reflects product epics and tasks
- 🧪 Multiple layers of testing for confidence and maintainability
