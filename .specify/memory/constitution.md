# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain, Configuration, Test). Cross-layer dependencies MUST be strictly unidirectional, flowing from higher layers to lower layers. Direct dependencies between non-adjacent layers are prohibited.

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities. Custom configurations MUST be minimal and clearly justified, typically within `src/main/java/org/springframework/samples/petclinic/system` or specific module configurations.

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed with accompanying unit and integration tests. Unit tests MUST focus on individual components, while integration tests MUST verify interactions between components and with external systems (e.g., database). Existing test suites (e.g., `src/test/java/org/springframework/samples/petclinic`) MUST be maintained and expanded.

### IV. Explicit Dependency Injection
All dependencies between Spring-managed beans MUST be explicitly declared using constructor injection or setter injection. Avoid field injection where possible to improve testability and clarity.

### V. Domain-Driven Design Principles
The core domain entities (e.g., `Owner`, `Pet`, `Vet`, `Visit`) MUST be the central focus. Business logic SHOULD reside within the domain or service layers, not directly in controllers or repositories.

## Additional Constraints

### Database Agnosticism
While integration tests may target specific databases (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`), the core application code MUST be designed to be database-agnostic, relying on Spring Data JPA abstractions.

### Internationalization (i18n)
All user-facing strings MUST be internationalized using Spring's message source mechanism. The `src/test/java/org/springframework/samples/petclinic/system/I18nPropertiesSyncTest.java` MUST pass to ensure all strings are translated across all supported locales.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to this constitution, code quality, test coverage, and architectural integrity.

### Branching Strategy
A Gitflow-like branching strategy is recommended, with `main` for production-ready code, `develop` for integration, and feature branches for new development.

### Dependency Management
All project dependencies MUST be managed via Maven (`pom.xml`). Explicit versioning is preferred over dynamic versioning to ensure build reproducibility.

## Governance

This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of core maintainers. Any approved amendments MUST include a migration plan for existing code and documentation. All pull requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-01 | **Last Amended**: 2026-09-01