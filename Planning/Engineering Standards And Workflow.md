

**Project:** SimplifyUI

**Scope:** Public, free SimplifyUI monorepo

**Status:** Planning baseline

**Last updated:** 23 November 2026

---

## 1. Purpose

This document establishes the engineering standards, development practices and repository workflows for SimplifyUI.

Its purpose is to ensure the project is developed with consistency, maintainability, reliability, security and long-term scalability in mind.

These standards apply to all contributors, including solo development.

The project should favour straightforward, well-structured solutions over unnecessary complexity. Engineering discipline should support development rather than create unnecessary overhead.

### Guiding principles

- SOLID

- DRY – Don't Repeat Yourself

- KISS – Keep It Simple

- YAGNI – You Aren't Gonna Need It

- Composition over inheritance

- High cohesion and low coupling

- Immutability where practical

- Type safety

- Testability first

- Explicit dependencies and clear package boundaries

- Accessibility and performance as core requirements


The guiding principle is:

**Build the simplest solution that reliably meets the requirements, while preserving the ability to extend and maintain it.**

---

## 2. Project Scope and Package Structure

SimplifyUI is a public monorepo containing the free packages that form the core UI ecosystem.

The planned package structure is:

```
packages/
├── shared/
├── theme/
├── icons/
├── layout/
├── desktop/
└── web/
```

### Package responsibilities

|Package|Responsibility|
|---|---|
|`@simplify-ui/shared`|Framework-independent shared utilities, types and foundations|
|`@simplify-ui/theme`|SimplifyPalette, themes, design tokens and theme utilities|
|`@simplify-ui/icons`|Shared icon library|
|`@simplify-ui/layout`|Shared layout foundations and reusable layout functionality|
|`@simplify-ui/desktop`|Desktop-oriented UI components|
|`@simplify-ui/web`|Web-oriented UI components|

Package boundaries should be deliberate.

- Shared foundations must not depend on higher-level UI packages.

- Framework-independent logic should remain separate from React-specific functionality wherever practical.

- Packages should expose deliberate public entry points.

- Internal implementation details should not become public APIs accidentally.

- Circular dependencies must be avoided.

- Dependencies between packages must be explicit.


### SimplifyUI Pro

SimplifyUI Pro will be developed in a completely separate monorepo.

The Pro ecosystem will install the published free SimplifyUI packages as dependencies.

Pro will extend the free ecosystem rather than duplicate or fork its implementation.

The free ecosystem must never depend on Pro.

Pro repository structure, engineering standards, release workflows and licensing arrangements are outside the scope of this document.

---

## 3. Development Toolchain

The project will use the following development tools.

|Tool|Purpose|
|---|---|
|pnpm|Package management and workspace management|
|Turborepo|Monorepo task orchestration and caching|
|TypeScript|Static typing and type safety|
|tsdown|Package building and bundling|
|Vitest|Unit and integration testing|
|React Testing Library|React component testing|
|Playwright|Browser and end-to-end testing|
|ESLint|Code quality and static analysis|
|Prettier|Consistent code formatting|
|Storybook|Isolated component development and documentation|
|Changesets|Package versioning and release management|

### Package management

pnpm will manage the monorepo and its workspaces.

Standards:

- Use pnpm consistently.

- Commit the lockfile.

- Use frozen lockfile installation in CI.

- Avoid unnecessary dependencies.

- Prefer workspace dependencies for internal packages.

- Keep dependency versions controlled and consistent.


### Build system

tsdown is the selected package bundler.

It will be used to build distributable package outputs and TypeScript declarations where appropriate.

The initial implementation must validate:

- ESM and CommonJS requirements.

- TypeScript declaration generation.

- Multiple package entry points.

- External dependencies and React peer dependencies.

- CSS handling.

- Tree-shaking.

- Compatibility with the intended package structure.


The first package build will act as the validation point. Configuration can be refined based on practical results.

### Runtime versions

Node.js and pnpm versions must be explicitly controlled.

The minimum supported Node.js version and package manager version will be established when the initial repository configuration is implemented.

CI must use the agreed versions consistently.

---

## 4. Coding Standards

Production code must be clear, concise, predictable and maintainable.

### General requirements

- Use TypeScript throughout the project.

- Prefer explicit types where they improve clarity and API safety.

- Avoid unnecessary abstractions and premature generalisation.

- Avoid duplicated logic where a shared implementation is justified.

- Prefer composition over inheritance.

- Avoid magic numbers and unexplained constants.

- Keep functions and modules focused.

- Avoid unnecessary state and side effects.

- Handle errors deliberately.

- Avoid circular dependencies.

- Keep public APIs intentional and stable.


### Package architecture

- Keep package responsibilities clearly defined.

- Separate framework-independent logic from framework-specific integration.

- Keep internal implementation details private.

- Expose functionality through deliberate public entry points.

- Avoid exposing internal types unless they are part of the intended public API.

- Prefer explicit dependency relationships.


### TypeScript

- Avoid `any` unless there is a documented and justified reason.

- Prefer `unknown` when the type is genuinely unknown.

- Use readonly types where appropriate.

- Prefer discriminated unions for state-dependent behaviour.

- Keep public types and interfaces documented.

- Avoid unnecessary type complexity.


### React components

- Components should have clear responsibilities.

- Prefer composition and reusable primitives.

- Avoid excessive prop complexity.

- Keep hooks focused on specific behaviour.

- Keep business logic outside rendering components where practical.

- Consider accessibility, keyboard interaction and focus management.

- Avoid unnecessary rendering and state updates.


### Performance

Performance is an important design consideration throughout SimplifyUI.

- Avoid unnecessary allocations and calculations.

- Use virtualisation where appropriate for large datasets.

- Avoid unnecessary React rendering.

- Keep expensive operations out of rendering paths.

- Use profiling and measurement before introducing optimisation complexity.


Performance-critical Pro functionality will require additional validation in its own development process.

---

## 5. Documentation Standards

Documentation is part of production quality, not an optional finishing step.

### Code documentation

Public types, interfaces and APIs must include appropriate documentation.

Documentation should explain:

- Purpose and responsibilities.

- Parameters and properties.

- Return values.

- Constraints and expected behaviour.

- Important defaults.

- Complex or non-obvious implementation decisions.


Not every private variable or trivial function requires a comment.

Comments should explain why something exists or behaves in a particular way, rather than simply restating the code.

### Module documentation

Modules should include a concise header identifying their purpose and responsibilities.

Documentation should remain readable and proportionate to the complexity of the module.

### Repository documentation

The repository must maintain:

- `README.md`

- `CONTRIBUTING.md`

- `CODE_OF_CONDUCT.md`

- `SECURITY.md`

- `LICENSE`


Additional documentation should cover:

- Architecture and package responsibilities.

- Installation and usage.

- Development setup.

- Testing and quality checks.

- Release procedures.


Package-level documentation should be provided where it materially improves discoverability and usability.

---

## 6. Branching Strategy

SimplifyUI will use **GitHub Flow**.

The `main` branch represents the stable, buildable state of the project.

Direct commits and pushes to `main` are prohibited.

All changes must enter `main` through pull requests.

This requirement applies even during solo development.

### Branch naming

Branches should use descriptive prefixes:

|Prefix|Purpose|
|---|---|
|`feat/`|New functionality|
|`fix/`|Bug fixes|
|`refactor/`|Code restructuring|
|`docs/`|Documentation changes|
|`chore/`|Maintenance and tooling|
|`test/`|Test-related changes|

Examples:

```
feat/theme-tokens
fix/button-disabled-state
refactor/shared-utilities
docs/architecture
chore/update-dependencies
test/grid-responsive-layout
```

### Branch lifetime

Feature branches may remain open for extended periods where necessary.

This is acceptable for a solo developer working on substantial features.

Short-lived branches should be used for small fixes and documentation changes.

Long-running feature branches should:

- Regularly incorporate changes from `main`.

- Prefer merging `main` into the feature branch.

- Avoid rebasing shared branches.

- Resolve conflicts before submitting for final review.

- Rerun relevant checks after synchronisation.


---

## 7. Commit Conventions

All commits should follow **Conventional Commits**.

Format:

```
type(scope): description
```

Examples:

```
feat(theme): add semantic colour tokens
fix(button): correct disabled state styling
refactor(shared): simplify class utilities
test(grid): add responsive layout tests
docs: update architecture documentation
chore: update development dependencies
```

Commit types should be meaningful and consistent.

Commits should represent logical changes rather than arbitrary editing sessions.

---

## 8. Pull Request Policy

All changes must be submitted through pull requests.

Pull requests are required regardless of whether the contributor is working alone or as part of a team.

This establishes a consistent development history and provides an opportunity to review changes before they enter `main`.

### Draft pull requests

Draft pull requests are encouraged for work in progress.

They allow:

- Early visibility of changes.

- Feedback before implementation is complete.

- CI validation during development.

- Discussion of architectural decisions.


Draft pull requests cannot be merged.

They must be marked as ready for review and satisfy all merge requirements before merging.

### Pull request requirements

A pull request should include:

1. Summary of the changes.

2. Reason for the changes.

3. Implementation details.

4. Testing performed.

5. Documentation updates.

6. Breaking changes, where applicable.


A pull request template will provide a consistent structure.

### Pull request checklist

Before merging, contributors should confirm:

- Implementation is complete.

- Code follows project standards.

- Relevant tests have been added or updated.

- Formatting and linting pass.

- Type checks pass.

- Builds pass.

- Documentation is updated.

- No unintended breaking changes are introduced.

- All review conversations are resolved.


### Merging

**Squash and merge** is the preferred merging strategy.

This keeps the `main` branch history clean and makes each merged pull request a logical unit of change.

### Reviews

During solo development, an independent approval will not be required.

The pull request requirement remains mandatory.

When additional contributors join, at least one approval should be required before merging.

---

## 9. Pull Request Labels

The repository will use a consistent set of labels.

|Label|Purpose|
|---|---|
|`feature`|New functionality|
|`bug`|Bug fixes|
|`documentation`|Documentation changes|
|`refactor`|Code restructuring|
|`breaking-change`|Changes that break compatibility|
|`dependencies`|Dependency updates|

Labels should make it easier to understand the purpose and impact of changes.

---

## 10. Code Quality and Testing

Quality checks must be automated wherever practical.

The project will use:

- Prettier for formatting.

- ESLint for code quality.

- TypeScript for static type checking.

- Vitest for unit and integration tests.

- React Testing Library for component behaviour.

- Playwright for browser and end-to-end testing.


### Testing principles

Tests should validate behaviour rather than implementation details.

Coverage expectations should reflect the responsibility and risk of each package.

|Area|Testing expectations|
|---|---|
|Shared utilities|Very high coverage|
|Theme and tokens|Comprehensive validation|
|Icons|Rendering and export validation|
|UI components|Behaviour, accessibility and interaction|
|Layout systems|Responsive and integration testing|
|Complex functionality|Performance and integration testing|

A single arbitrary coverage percentage will not be imposed across every package.

Code coverage should be measured and reported, with a coverage service considered if it provides sufficient value.

### Required quality checks

Pull requests must pass:

1. Formatting validation.

2. ESLint.

3. TypeScript type checking.

4. Relevant automated tests.

5. Relevant package builds.


### Affected package execution

Turborepo will be used to execute tasks efficiently across the monorepo.

Where supported and correctly configured, CI should run checks only for affected packages and their dependants.

Changes to root configuration, workspace configuration, lockfiles or shared foundations may require broader validation.

The exact affected-package commands and dependency behaviour must be validated during implementation.

---

## 11. GitHub Actions

GitHub Actions will automate quality checks, security checks and releases.

The workflow architecture should remain simple and maintainable.

Four separate workflows are planned.

### 11.1 Pull Request CI

**Essential from the outset.**

Runs when a pull request is opened, updated or marked ready for review.

Responsibilities:

- Install dependencies.

- Validate formatting.

- Run ESLint.

- Run TypeScript checks.

- Run relevant tests.

- Build affected packages.


Successful completion is required before merging.

### 11.2 Main Branch Validation

**Essential from the outset.**

Runs after changes are merged into `main`.

Responsibilities:

- Validate the integrated repository.

- Run relevant quality checks.

- Confirm package builds.

- Detect integration issues.


### 11.3 Security and Dependency Checks

**Essential from the outset.**

Responsibilities:

- Dependency vulnerability checks.

- CodeQL analysis.

- Dependency security monitoring.

- GitHub security integrations.

- Workflow security validation.


Security checks should be configured to run independently of ordinary PR validation where appropriate.

### 11.4 Release and Publishing

**Introduced when package publishing begins.**

Responsibilities:

- Process Changesets.

- Prepare version updates.

- Generate changelogs.

- Build packages.

- Publish approved packages to npm.

- Create GitHub releases where appropriate.


Release publishing must remain separate from ordinary CI.

### Workflow standards

- Use GitHub-hosted runners initially.

- Use least-privilege workflow permissions.

- Default to read-only permissions where possible.

- Pin third-party GitHub Actions to full commit SHAs.

- Keep secrets restricted to trusted workflows.

- Avoid privileged workflows on untrusted pull requests.

- Avoid `pull_request_target` for ordinary build and test workflows.

- Use frozen lockfile installation.

- Control Node.js and pnpm versions.

- Cancel obsolete workflow runs where appropriate.

- Keep required status check names stable.

- Reuse workflow logic where it reduces duplication without adding unnecessary complexity.


Remote caching can be considered later.

---

## 12. Security Standards

Security is a core engineering requirement.

Since the SimplifyUI repository is public, GitHub's free security features will be used wherever available.

### GitHub security features

The following features should be enabled:

|Feature|Purpose|
|---|---|
|Dependabot alerts|Identify vulnerable dependencies|
|Dependabot security updates|Propose automated security fixes|
|Dependency graph|Track project dependencies|
|CodeQL|Analyse source code for security vulnerabilities|
|Secret scanning|Detect accidentally committed credentials|
|Push protection|Help prevent secrets being committed|

### Additional security practices

- Keep dependencies updated.

- Review dependency update pull requests.

- Avoid unnecessary third-party dependencies.

- Never commit API keys, tokens or credentials.

- Use environment secrets appropriately.

- Apply least-privilege access.

- Review GitHub Actions permissions.

- Keep repository access restricted to trusted contributors.

- Maintain a `SECURITY.md` file explaining how to report vulnerabilities.


GitHub security feature availability should be verified against the repository's current plan and settings during setup.

Security should be built into the development process rather than treated as a final release check.

---

## 13. Repository Protection

The `main` branch must be protected.

The following protections should be configured:

- Require pull requests before merging.

- Prevent direct pushes.

- Prevent force pushes.

- Require successful CI checks.

- Require resolved review conversations.

- Require approval when additional contributors join.

- Enforce the agreed merge strategy.


Linear history may be enabled if compatible with the chosen squash-merging configuration.

Branch protection must be configured to support solo development without introducing an approval requirement that cannot be satisfied.

---

## 14. Versioning and Release Management

SimplifyUI will use **Semantic Versioning (SemVer)**.

Version format:

```
MAJOR.MINOR.PATCH
```

|Version change|Meaning|
|---|---|
|MAJOR|Breaking changes|
|MINOR|Backwards-compatible functionality|
|PATCH|Backwards-compatible fixes|

### Independent package versioning

Each package will have its own version.

For example:

```
@​simplify-ui/shared     1.2.0
@​simplify-ui/theme      1.1.0
@​simplify-ui/icons      1.0.2
@​simplify-ui/layout     1.0.0
@​simplify-ui/desktop    1.3.0
@​simplify-ui/web        1.1.0
```

Packages should only receive new versions when their own changes require them.

This avoids unnecessary releases and allows packages to evolve independently.

### Changesets

Changesets will manage:

- Version updates.

- Release notes.

- Package changelogs.

- Release preparation.

- Package dependency version updates where required.


Changesets should be added when a pull request introduces a change that affects a published package.

Documentation-only or internal changes that do not affect published packages do not necessarily require a changeset.

### Publishing

The free SimplifyUI packages will be published publicly through npm.

Publishing will be automated through a dedicated GitHub Actions release workflow.

The workflow must:

- Process approved changesets.

- Determine package version changes.

- Build packages.

- Publish the appropriate packages.

- Preserve package dependency compatibility.

- Produce release records and changelogs.


The exact publishing permissions and authentication method will be finalised during implementation.

---

## 15. README and Repository Badges

The README should provide a clear introduction to SimplifyUI and communicate the project's status.

A compact horizontal badge row will appear directly below the project title and short description.

Planned badges:

- Build status.

- Test status.

- Code coverage.

- Licence.

- TypeScript.

- pnpm.


Shields.io will be used to provide badges.

Badges should link to meaningful project information where appropriate.

Their values should be generated from reliable sources rather than maintained manually.

Additional badges, such as Storybook or package versions, may be introduced when they provide useful information.

---

## 16. Repository Governance Files

The repository will maintain the following governance files:

|File|Purpose|
|---|---|
|`README.md`|Project introduction and usage|
|`CONTRIBUTING.md`|Contribution and development instructions|
|`CODE_OF_CONDUCT.md`|Expected contributor behaviour|
|`SECURITY.md`|Security vulnerability reporting|
|`LICENSE`|Project licensing terms|

GitHub issue templates and pull request templates will also be established.

These files should be maintained as the project evolves.

The licensing arrangements for individual packages must be consistent with the intended free ecosystem distribution model.

---

## 17. Implementation Priorities

The standards in this document define the intended approach. Some technical details must still be validated during implementation.

The initial implementation should proceed in a controlled order.

### Foundation

- Establish the pnpm workspace.

- Configure TypeScript.

- Configure Turborepo.

- Configure tsdown.

- Establish shared ESLint and Prettier configuration.

- Establish testing infrastructure.

- Define package boundaries and entry points.


### Repository workflow

- Configure GitHub Flow.

- Protect `main`.

- Create branch and PR templates.

- Configure pull request labels.

- Establish GitHub Actions CI workflows.

- Configure repository governance files.


### Security

- Enable Dependabot.

- Enable CodeQL.

- Enable secret scanning and push protection.

- Configure dependency auditing.

- Validate workflow permissions and security.


### Release infrastructure

- Configure Changesets.

- Establish independent package versioning.

- Configure npm publishing.

- Establish automated release workflows.

- Add README status badges.


### Validation

The first packages should be used to validate the architecture and tooling before applying the configuration across the entire monorepo.

In particular, the first package build should validate tsdown, declaration generation, package exports and dependency handling.

---

## 18. Decisions and Future Review

This document records the agreed engineering baseline for the free SimplifyUI ecosystem.

The following details remain subject to implementation validation:

- Minimum supported Node.js version.

- Exact pnpm version.

- Exact Turborepo task configuration.

- tsdown build configuration.

- Package export and declaration strategy.

- Coverage reporting implementation.

- Exact GitHub Actions workflow triggers and job structure.

- npm publishing authentication and permissions.

- Final package licensing details.


These are implementation decisions, not reasons to delay establishing the agreed architecture and workflow.

Standards may be revised when practical experience demonstrates a better approach.

Changes should be deliberate and documented rather than introduced inconsistently.

---

## 19. Final Guiding Principle

SimplifyUI should be engineered to a professional standard without becoming unnecessarily complicated.

The project should prioritise:

- Clear architecture.

- Small, focused implementations.

- Reliable behaviour.

- Strong testing.

- Consistent documentation.

- Secure development practices.

- Predictable releases.

- Maintainable package boundaries.


**Quality should come from good engineering decisions, not from adding complexity for its own sake.**