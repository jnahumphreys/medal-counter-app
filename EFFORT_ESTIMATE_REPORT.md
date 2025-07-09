# Medal Counter App MVP Work-Breakdown & Effort-Estimate Report

A structured work-breakdown of every open GitHub issue mapped to the MVP Product-Requirements Document (PRD), with engineering-hour **and story-point** estimates, contingency allowance, and an aggregate timeline to inform scope, resourcing, and schedule decisions.

**Resourcing assumption:** Estimates are based on one staff-level engineer working solo; estimates may shrink if work streams can run in parallel or if additional engineers join the effort.

---

## Breakdown

| Seq | GitHub Issue / Task | Type      | Est. hrs | **SP** |
| --- | ------------------- | --------- | -------- | ------ |
| 1   | Lock commits to main branch and enforce approved PR’s ([#12](https://github.com/jnahumphreys/medal-counter-app/issues/12)) | Dev-Ops   | **0.25** | **1** |
| 2   | Add DevContainer support and baseline configuration ([#1](https://github.com/jnahumphreys/medal-counter-app/issues/1)) | Dev-Ops   | **0.25** | **1** |
| 3   | Scaffold project using Vite + TypeScript ([#2](https://github.com/jnahumphreys/medal-counter-app/issues/2)) | Dev-Ops   | **0.25** | **1** |
| 4   | Configure ESLint, Prettier, and Husky ([#3](https://github.com/jnahumphreys/medal-counter-app/issues/3)) | Dev-Ops   | **0.25** | **1** |
| 5   | Add initial GitHub Actions workflow for version bumping, linting, formatting, and Jest tests ([#5](https://github.com/jnahumphreys/medal-counter-app/issues/5)) | Dev-Ops   | **0.25** | **1** |
| 6   | Set up Jest and baseline unit test infrastructure ([#4](https://github.com/jnahumphreys/medal-counter-app/issues/4)) | Dev-Ops   | **0.25** | **1** |
| 7   | Create Zustand base store ([#15](https://github.com/jnahumphreys/medal-counter-app/issues/15)) | Front-end | **1**    | **2** |
| 8   | Create Zustand entrantsSlice ([#52](https://github.com/jnahumphreys/medal-counter-app/issues/52)) | Front-end | **1**    | **2** |
| 9   | Implement app initialiser to fetch data ([#17](https://github.com/jnahumphreys/medal-counter-app/issues/17)) | Front-end | **1**    | **2** |
| 10  | Create useSortedMedals() hook ([#19](https://github.com/jnahumphreys/medal-counter-app/issues/19)) | Front-end | **1**    | **2** |
| 11  | Install, setup and configure TailwindCSS ([#6](https://github.com/jnahumphreys/medal-counter-app/issues/6)) | Dev-Ops   | **0.5**  | **1** |
| 12  | Install, setup and configure Storybook ([#7](https://github.com/jnahumphreys/medal-counter-app/issues/7)) | Dev-Ops   | **0.5**  | **1** |
| 13  | Add Storybook test runner to GitHub Actions PR workflow ([#9](https://github.com/jnahumphreys/medal-counter-app/issues/9)) | Dev-Ops   | **0.5**  | **1** |
| 14  | Create pure Flag component ([#20](https://github.com/jnahumphreys/medal-counter-app/issues/20)) | Front-end | **1**    | **2** |
| 15  | Create EntrantListItem pure component ([#21](https://github.com/jnahumphreys/medal-counter-app/issues/21)) | Front-end | **1**    | **2** |
| 16  | Create pure EntrantsList component ([#22](https://github.com/jnahumphreys/medal-counter-app/issues/22)) | Front-end | **1**    | **2** |
| 17  | Create AppTitle component ([#23](https://github.com/jnahumphreys/medal-counter-app/issues/23)) | Front-end | **0.5**  | **1** |
| 18  | Create pure MainView presentational component ([#50](https://github.com/jnahumphreys/medal-counter-app/issues/50)) | Front-end | **1**    | **2** |
| 19  | Create connected EntrantsList Container component ([#24](https://github.com/jnahumphreys/medal-counter-app/issues/24)) | Front-end | **1**    | **2** |
| 20  | Create pure MainView container component ([#51](https://github.com/jnahumphreys/medal-counter-app/issues/51)) | Front-end | **1**    | **2** |
| 21  | Create App component ([#25](https://github.com/jnahumphreys/medal-counter-app/issues/25)) | Front-end | **1**    | **2** |
| 22  | Create main index.ts entry point ([#26](https://github.com/jnahumphreys/medal-counter-app/issues/26)) | Front-end | **1**    | **2** |
| 23  | Add App build GitHub Actions PR workflow ([#10](https://github.com/jnahumphreys/medal-counter-app/issues/10)) | Dev-Ops   | **1**    | **2** |
| 24  | Install, setup and configure Cypress ([#8](https://github.com/jnahumphreys/medal-counter-app/issues/8)) | Dev-Ops   | **1**    | **2** |
| 25  | Add Cypress E2E test runner to GitHub Actions PR workflow ([#11](https://github.com/jnahumphreys/medal-counter-app/issues/11)) | Dev-Ops   | **1**    | **2** |
| 26  | Add E2E tests for initial rendering of Olympic entrants results (happy path) ([#29](https://github.com/jnahumphreys/medal-counter-app/issues/29)) | QA        | **1**    | **2** |
| 27  | Implement Zustand sortSlice ([#16](https://github.com/jnahumphreys/medal-counter-app/issues/16)) | Front-end | **1**    | **2** |
| 28  | Create sortMedals() utility with tie-break logic ([#18](https://github.com/jnahumphreys/medal-counter-app/issues/18)) | Front-end | **1**    | **2** |
| 29  | Create useSortedMedals custom React hook ([#53](https://github.com/jnahumphreys/medal-counter-app/issues/53)) | Front-end | **1**    | **2** |
| 30  | Create pure SortByMedal button component ([#32](https://github.com/jnahumphreys/medal-counter-app/issues/32)) | Front-end | **1**    | **2** |
| 31  | Create pure SortByTitle presentational component ([#49](https://github.com/jnahumphreys/medal-counter-app/issues/49)) | Front-end | **1**    | **2** |
| 32  | Create pure SortEntrants component ([#31](https://github.com/jnahumphreys/medal-counter-app/issues/31)) | Front-end | **1**    | **2** |
| 33  | Create connected SortByGold container component ([#34](https://github.com/jnahumphreys/medal-counter-app/issues/34)) | Front-end | **1**    | **2** |
| 34  | Create connected SortBySilver container component ([#35](https://github.com/jnahumphreys/medal-counter-app/issues/35)) | Front-end | **1**    | **2** |
| 35  | Create connected SortByBronze container component ([#36](https://github.com/jnahumphreys/medal-counter-app/issues/36)) | Front-end | **1**    | **2** |
| 36  | Create connected SortByTotal container component ([#37](https://github.com/jnahumphreys/medal-counter-app/issues/37)) | Front-end | **1**    | **2** |
| 37  | Create connected SortEntrants container component ([#48](https://github.com/jnahumphreys/medal-counter-app/issues/48)) | Front-end | **1**    | **2** |
| 38  | Add SortEntrants container component to App layout ([#38](https://github.com/jnahumphreys/medal-counter-app/issues/38)) | Front-end | **1**    | **2** |
| 39  | Add E2E tests for sorting Olympic entrants by medal or title ([#39](https://github.com/jnahumphreys/medal-counter-app/issues/39)) | QA        | **1**    | **2** |
| 40  | Implement logic to read, validate and initialise sorting from URL query param ([#40](https://github.com/jnahumphreys/medal-counter-app/issues/40)) | Front-end | **1**    | **2** |
| 41  | Implement logic to update URL query param on change of sort option ([#41](https://github.com/jnahumphreys/medal-counter-app/issues/41)) | Front-end | **1**    | **2** |
| 42  | Add E2E tests for sorting medals using query params ([#42](https://github.com/jnahumphreys/medal-counter-app/issues/42)) | QA        | **1**    | **2** |
| 43  | Add E2E tests for updating URL query param on change of sort value ([#43](https://github.com/jnahumphreys/medal-counter-app/issues/43)) | QA        | **1**    | **2** |
| 44  | Create pure ErrorFeedback UI component ([#44](https://github.com/jnahumphreys/medal-counter-app/issues/44)) | Front-end | **1**    | **2** |
| 45  | Create connected HOC ErrorFeedback component ([#45](https://github.com/jnahumphreys/medal-counter-app/issues/45)) | Front-end | **1**    | **2** |
| 46  | Add required error handling to Zustand state, fetch logic and query param logic ([#46](https://github.com/jnahumphreys/medal-counter-app/issues/46)) | Front-end | **1**    | **2** |
| 47  | Add required E2E tests for ErrorFeedback ([#47](https://github.com/jnahumphreys/medal-counter-app/issues/47)) | QA        | **1**    | **2** |
|    | **Subtotal**              |           | **40.5** h | **84 SP** |
|    | **Contingency (+15%)**    |           | **+6 h** | *(n/a)* |
|    | **Projected total**       |           | **≈ 46.5 h** | **≈ 84 SP** |

---

## Phase snapshot

| Phase                  | Major activities | Approx. calendar time* |
| ---------------------- | ---------------- | ----------------------- |
| Epic 13: Setup initial local development environment and GitHub repository | Seq 1-5         | 0.5 days                   |
| Epic 14: allow a user to view a list of Olympic entrants results           | Seq 6-26        | 4 days                 |
| Epic 27: allow a user to sort Olympic entrants by medal or title           | Seq 27-39        | 3 days                   |
| Epic 28: allow a user to sync sorting using URL query parameter            | Seq 40 - 43 | 1 day                 |
| Epic 30: allow a user to identify when an application error has occurred   | Seq 44-47        | 1 day                 |
| **Total**              |                  | **~9.5 working days**   |

*Assumes ~5 focused hours/day.

---

## Notes
- Estimates are based on current open issues and may change as requirements evolve.
- Story points (SP) are relative and used for planning, not absolute effort.
- Contingency is included to account for unknowns and integration overhead.

---
