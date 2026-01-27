# Coding Standards & Contribution

We follow strict engineering standards to ensure maintainability.

## ☕️ Backend (Java/Spring)

-   **Style**: Google Java Style Guide.
-   **Architecture**: Controller -> Service -> Repository.
-   **Testing**: Unit tests for Services (`@ExtendWith(MockitoExtension.class)`).
-   **Git**: Feature branches (`feat/feature-name`).

## ⚛️ Frontend (React/Next.js)

-   **Style**: Prettier + ESLint (Standard config).
-   **Components**:
    -   Use `PascalCase` for components.
    -   Use `kebab-case` for file names in `app/`.
-   **Types**: Strict TypeScript usage (No `any`).

## 🔄 Workflow

1.  **Fork** the repository.
2.  **Clone** locally.
3.  **Branch**: `git checkout -b feat/my-feature`
4.  **Commit**: Conventional Commits (e.g., `feat: add api endpoint`).
5.  **PR**: Open Pull Request against `main`.
