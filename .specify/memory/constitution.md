# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain, Configuration, Test). Direct dependencies MUST only flow downwards (e.g., Controller can depend on Service, Service can depend on Repository, but not vice-versa). This ensures maintainability and separation of concerns.

### II. Spring Boot Conventions
The project MUST leverage Spring Boot features and conventions for configuration, dependency injection, and application bootstrapping. This includes using annotations like `@SpringBootApplication`, `@Controller`, `@Repository`, and managing beans through Spring's context.

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed with a test-first approach. Unit tests MUST cover individual components, integration tests MUST verify interactions between layers and external systems (like databases), and end-to-end tests (where applicable) MUST validate user flows. The existing test suite, covering controllers, services, and models, MUST be maintained and expanded.

### IV. Data Persistence Abstraction
Data access logic MUST be encapsulated within repository interfaces, leveraging Spring Data JPA. Direct SQL queries or manual persistence management within service or controller layers are forbidden. The use of `Pageable` for data retrieval MUST be employed for efficient handling of large datasets.

### V. Internationalization (i18n) and Localization
All user-facing strings MUST be externalized into resource bundles (`messages.properties` and its language variants). The `I18nPropertiesSyncTest` MUST pass, ensuring all strings are translated across all supported locales.

## Additional Constraints

The project MUST adhere to Java Bean Validation standards for data integrity.
The project MUST utilize Jakarta Persistence API (JPA) for object-relational mapping.
The project MUST support multiple database integrations as evidenced by `MySqlIntegrationTests` and `PostgresIntegrationTests`.
The project MUST be containerizable, as indicated by the presence of a `k8s/` directory.
The project MUST support development environments via Dev Containers, as indicated by the `.devcontainer/` directory.

## Development Workflow

Code changes MUST be submitted via Pull Requests (PRs).
All PRs MUST include sufficient unit and/or integration tests.
PRs MUST be reviewed by at least one other team member.
Automated checks (CI pipeline) MUST pass before merging.
The project utilizes Spring Boot's auto-configuration and dependency management.

## Governance

This Constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository.
Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team.
All Pull Requests and code reviews MUST verify compliance with the principles outlined in this Constitution.
Any deviation from these principles MUST be explicitly justified and approved.

**Version**: 1.0.0 | **Ratified**: 2026-09-03 | **Last Amended**: 2026-09-03