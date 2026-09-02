# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test, System). Direct dependencies MUST only flow downwards (e.g., Controllers can depend on Services and Repositories, but not vice-versa).

### II. Spring Boot Conventions
The project MUST leverage Spring Boot's auto-configuration capabilities and follow established Spring conventions for dependency injection, component scanning, and configuration management. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be clearly defined and adhere to Spring's declarative style.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST verify individual component logic, while integration tests MUST validate interactions between components and with external systems (e.g., databases via `MySqlIntegrationTests`, `PostgresIntegrationTests`). Test coverage MUST be maintained at a high level, with specific attention to controller endpoints and service layer operations.

### IV. Data Persistence Abstraction
The project MUST utilize Spring Data JPA for data access. Repository interfaces (e.g., `OwnerRepository`, `VetRepository`) MUST abstract the underlying persistence mechanism, allowing for easier testing and potential future database migrations.

### V. Internationalization (i18n) Compliance
All user-facing strings MUST be externalized and managed through properties files. The `I18nPropertiesSyncTest` MUST pass, ensuring that all strings are translated across all supported locales and that no hard-coded strings exist in the UI layer.

## Development Workflow

The standard development workflow involves:
1.  **Feature/Bug Identification**: Clearly define the scope of work.
2.  **Branching**: Create a new feature branch from the main development branch.
3.  **Development**: Implement the feature or fix the bug, adhering to the Core Principles. Write comprehensive unit and integration tests *before* or *concurrently* with implementation.
4.  **Code Review**: Submit a Pull Request (PR) for review by at least one other team member. The review MUST verify adherence to this constitution, code quality, and test coverage.
5.  **Testing**: All automated tests (unit, integration) MUST pass. Manual testing may be required for critical user flows.
6.  **Merging**: Once approved and all checks pass, the PR can be merged into the main development branch.

## Governance

This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a migration plan to ensure existing code and processes are updated accordingly. All Pull Requests and code reviews MUST verify compliance with this constitution. Complexity MUST always be justified.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02