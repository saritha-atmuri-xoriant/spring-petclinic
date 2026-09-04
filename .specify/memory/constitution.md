# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain, Configuration, Test). Direct dependencies MUST only flow downwards (e.g., Controller can depend on Service, Service on Repository, but not vice-versa). This ensures maintainability and clear separation of concerns.

### II. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed using TDD. Unit tests MUST cover individual components, integration tests MUST validate interactions between components and external systems (e.g., database), and end-to-end tests MUST verify user flows. The existing test suite, including `MySqlIntegrationTests`, `PostgresIntegrationTests`, and various controller/service tests, MUST be maintained and expanded.

### III. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be minimal, well-documented, and adhere to Spring best practices. Dependencies MUST be managed via Maven.

### IV. Domain-Driven Design Principles
The core domain entities (`Owner`, `Pet`, `Vet`, `Visit`, `PetType`, `Specialty`) MUST be clearly defined and immutable where appropriate. Business logic MUST be encapsulated within the domain or service layers, not directly within controllers or repositories. Validation MUST be handled using Jakarta Bean Validation annotations and custom validators (`PetValidator`).

### V. Observability and Internationalization
The application MUST support internationalization (i18n) as evidenced by `WebConfiguration` and `I18nPropertiesSyncTest`. All user-facing strings MUST be externalized into resource bundles. Logging and error handling mechanisms SHOULD be implemented to facilitate debugging and monitoring.

## Additional Constraints

The project MUST utilize Java as the primary programming language and Maven for dependency management. The application is designed to run on a Java Virtual Machine and is compatible with standard relational databases (e.g., MySQL, PostgreSQL) as indicated by integration tests. Containerization configurations (e.g., `k8s/`, `.devcontainer/`) SHOULD be maintained for deployment and development consistency.

## Development Workflow

All code changes MUST be submitted as Pull Requests (PRs). Each PR MUST include comprehensive unit and integration tests. Code reviews are mandatory, with at least one reviewer approving the changes. CI/CD pipelines MUST automatically run all tests and static analysis checks before merging.

## Governance

This Constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of core maintainers. A migration plan MUST be provided for any changes that impact existing workflows or code. All Pull Requests and code reviews MUST verify compliance with these principles.

**Version**: 1.0.0 | **Ratified**: 2026-09-04 | **Last Amended**: 2026-09-04