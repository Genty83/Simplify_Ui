# Contributing to SimplifyUI

## 1. Purpose

This document defines the development workflow and engineering practices used when building and maintaining SimplifyUI.

Initially, it serves as the project's internal development guide. It establishes consistent standards for planning, implementation, testing, documentation and code review.

## 2. Engineering Principles

Development should follow these principles:

- **SOLID** – maintain clear responsibilities and well-defined boundaries.
- **DRY** – avoid unnecessary duplication.
- **KISS** – favour straightforward, understandable solutions.
- **YAGNI** – implement only what is currently justified.
- **Composition over inheritance** – favour composable and reusable designs.
- **High cohesion and low coupling** – keep related responsibilities together and minimise unnecessary dependencies.
- **Immutability** – prefer immutable data and predictable state changes.
- **Testability** – design software so that behaviour can be tested independently.

Avoid unnecessary abstractions, premature optimisation and over-engineering.

## 3. Planning and Design

Significant work should be planned before implementation.

- Record architectural decisions and relevant design considerations.
- Define package responsibilities and dependency boundaries.
- Consider maintainability, accessibility and extensibility.
- Prefer established project conventions over introducing new patterns without justification.
- Keep planning and implementation documentation up to date.

Changes to architecture or shared package contracts should be considered carefully because they may affect multiple applications and packages.

## 4. Development Environment

The repository uses the following core tooling:

- Node.js 26.
- pnpm 12.23.0.
- TypeScript.
- Turborepo.
- Git and GitHub.

Use the versions specified by the repository configuration.

Install dependencies using pnpm and respect the existing workspace structure. Avoid introducing alternative package managers or unnecessary dependencies.

## 5. Git Workflow

All development work should take place on a dedicated branch.

Use descriptive branch names with a suitable category prefix:

| Prefix | Purpose |
|---|---|
| `feat/` | New functionality |
| `fix/` | Bug fixes |
| `chore/` | Maintenance and repository configuration |
| `docs/` | Documentation changes |
| `refactor/` | Code restructuring |
| `test/` | Test-related changes |
| `ci/` | Continuous integration changes |

Examples:

- `feat/theme-tokens`
- `fix/grid-layout`
- `docs/update-contributing-guide`
- `chore/github-templates`

Do not commit routine development work directly to `main`.

## 6. Commit Messages

Commit messages must follow the Conventional Commits specification.

Use the format:

`type(scope): description`

Examples:

- `feat(theme): add semantic colour tokens`
- `fix(layout): correct responsive sizing`
- `docs(repo): add contribution guidelines`
- `chore(ci): update workflow configuration`

Commit messages should be concise and describe the purpose of the change.

## 7. Pull Requests

All changes must be submitted through a pull request, including changes made during solo development.

Pull requests should:

- Have a clear and descriptive title.
- Explain the purpose and scope of the changes.
- Identify important implementation details.
- Describe testing performed.
- Include relevant documentation updates.
- Avoid unrelated changes.

Use the repository pull request template.

Before merging:

- Required GitHub Actions checks must pass.
- Changes should be reviewed for correctness and unnecessary complexity.
- All review conversations must be resolved where applicable.
- The pull request must satisfy the repository's branch protection rules.

Use squash merging to maintain a clean and readable main branch history.

## 8. Testing and Quality

Changes should be tested at the appropriate level.

Depending on the affected functionality, this may include:

- Unit tests.
- Integration tests.
- Type checking.
- Linting.
- Build verification.
- Manual testing where appropriate.

Do not consider a change complete until relevant checks have passed.

Avoid introducing functionality without appropriate test coverage. The level of testing should be proportionate to the change.

## 9. Documentation

Documentation should explain public behaviour, intended usage and relevant design decisions.

- Update documentation when behaviour or public interfaces change.
- Keep examples accurate and maintainable.
- Document architectural decisions where they affect future development.
- Avoid excessive comments or documentation that simply repeats the implementation.
- Keep planning documents aligned with the current project direction.

## 10. Dependencies

New dependencies should be introduced only when there is a clear benefit.

Before adding a dependency, consider:

- Whether the functionality can reasonably be implemented using existing tools.
- Package size and runtime impact.
- Maintenance activity and long-term support.
- Licence compatibility.
- Security implications.

Prefer existing workspace packages where appropriate.

## 11. Definition of Done

A change is considered complete when:

- The implementation meets its intended requirements.
- Engineering standards have been followed.
- Relevant tests and quality checks pass.
- Documentation has been updated where necessary.
- The pull request has passed required CI checks.
- The pull request has been merged into `main`.