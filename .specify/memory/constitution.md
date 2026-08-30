# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). No cross-layer dependencies are permitted except for those explicitly defined by the framework (e.g., Controller depending on Service, Service depending on Repository).

### II. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal and clearly justified, adhering to established Spring Boot patterns.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and/or integration tests. Unit tests MUST cover individual components (e.g., `OwnerControllerTests.java`, `PetValidatorTests.java`), while integration tests MUST verify interactions between layers and external systems (e.g., `MySqlIntegrationTests.java`, `CrashControllerIntegrationTests.java`). Test coverage MUST be maintained above 80%.

### IV. Data Persistence Abstraction
The project MUST utilize Spring Data JPA for data access. Repository interfaces (e.g., `OwnerRepository.java`, `VetRepository.java`) MUST abstract the underlying persistence mechanism, ensuring that domain entities are not directly coupled to database specifics.

### V. Internationalization and Localization
All user-facing strings MUST be externalized and managed through properties files (e.g., `messages.properties`). The `I18nPropertiesSyncTest.java` MUST pass to ensure all strings are translated across all supported locales.

## Development Workflow

The standard development workflow involves:
1. **Feature Branching**: All development MUST occur on feature branches.
2. **Code Review**: All Pull Requests (PRs) MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to this constitution, code quality, and test coverage.
3. **Automated Testing**: CI pipelines MUST execute all unit and integration tests on every commit.
4. **Deployment**: Deployments to production environments are subject to successful completion of all automated tests and a final sign-off from the lead architect.

## Governance

This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a migration plan to ensure existing code adheres to the new principles. All Pull Requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-30 | **Last Amended**: 2026-08-30