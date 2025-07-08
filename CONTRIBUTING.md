# Contributing to Olympic Medal Counter

Thank you for considering contributing to this open-source project!  
We welcome thoughtful contributions that improve functionality, design, accessibility, or code clarity.

---

## 📌 Before You Start

Please follow these guidelines to ensure smooth collaboration:

- 🔍 **Open an issue first** to propose changes or report bugs.  
- 💬 Use the issue to clarify requirements and ensure alignment before starting work.
- 📌 All contributions should be tied to a GitHub issue and tracked through a pull request.

---

## 📂 Branching Strategy

- Work should branch off of the `main` branch.
- Use feature branches for new functionality (e.g. `feature/123-sort-buttons`).
- Branch names **must reference the associated GitHub issue** (e.g. include `123` if it's issue #123).

---

## 📥 Development Setup

### Prerequisites
- Todo

### Clone and Install
- Todo

### DevContainers
- This project supports [DevContainers](https://containers.dev/).
- If using VS Code, open the project in a containerized environment for consistency.

---

## ✅ Code Standards

### Commit Conventions
- We use [Conventional Commits](https://www.conventionalcommits.org/) (`feat:`, `fix:`, `chore:`, etc.).
- Include the GitHub issue number in your commit message (e.g. `feat: add bronze sort button (#45)`).

### Linting and Formatting
Pre-commit hooks (via [Husky](https://typicode.github.io/husky)) enforce linting and formatting.

### Run manually:
- Todo

---

## 🧪 Testing Requirements

All code contributions **must include appropriate tests**. The following applies:

### UI Components
- Must include a [Storybook](https://storybook.js.org/) story.
- Should be covered by the Storybook Test Runner (`.test.tsx`).
- Should present **all available visual states** (e.g. active/inactive, disabled).

### Business Logic
- Must include unit tests (where applicable).
- Functions in `utils/` or hooks in `hooks/` must be isolated and tested.

### Run All Tests
- Todo

---

## 📦 Versioning

- This project uses **Semantic Versioning (SemVer)**.
- If your contribution introduces a new feature or fix, include an appropriate version bump in your PR (`minor`, `patch`, or `major` depending on impact).

---

## ✅ Pull Request Checklist

Before submitting your PR:

- [ ] The related GitHub issue is referenced in the PR title/description.
- [ ] All required tests pass locally.
- [ ] Pre-commit hooks have passed.
- [ ] Storybook stories and test cases are included (if UI).
- [ ] Code follows project conventions (naming, formatting, commit style).
- [ ] Applicable version bump is included.

---

## 🙌 Thank You!

Your time and effort are greatly appreciated.  
If in doubt, open an issue or draft PR — we’re happy to help guide you through the process.
