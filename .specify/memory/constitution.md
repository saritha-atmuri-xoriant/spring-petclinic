# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Direct dependencies MUST only flow downwards (e.g., Controllers depend on Services, Services depend on Repositories). No cross-layer dependencies are permitted outside of the defined flow.

### II. Spring Boot Convention and Best Practices
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Configuration MUST be managed via `application.properties` or `@Configuration` classes. Dependency Injection MUST be used for managing component lifecycles and collaborations.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components in isolation, while integration tests MUST verify interactions between components and with external systems (e.g., database). Test coverage MUST be maintained at a minimum of 80%.

### IV. Data Persistence Abstraction
Data access MUST be abstracted through Spring Data JPA repositories. All database interactions MUST be performed via these repositories, ensuring a consistent and maintainable data access layer. Direct SQL queries within business logic are prohibited.

### V. Internationalization and Localization
All user-facing text strings MUST be externalized into resource bundles (`.properties` files) and managed through Spring's i18n mechanisms. The `I18nPropertiesSyncTest` MUST pass to ensure all strings are translated across all supported locales.

## Additional Constraints

The project MUST utilize Java 17 or later.
The project MUST be buildable using Maven.
The project MUST support multiple database integrations (e.g., H2, MySQL, PostgreSQL) as demonstrated by existing integration tests.
Containerization configurations (e.g., Dockerfile, Kubernetes manifests) MUST be maintained in the `k8s/` directory.

## Development Workflow

Code changes MUST be submitted via Pull Requests (PRs).
All PRs MUST undergo a code review by at least one other team member.
Automated checks (CI pipeline) MUST pass before merging a PR. These checks include compilation, unit tests, integration tests, and static code analysis.
Feature development SHOULD follow an iterative approach, with frequent commits and small, manageable PRs.

## Governance

This Constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository.
Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. A migration plan MUST be provided for any significant changes.
All Pull Requests and code reviews MUST verify compliance with the principles outlined in this Constitution.
Any deviation from these principles MUST be explicitly justified and approved.

**Version**: 1.0.0 | **Ratified**: 2026-08-29 | **Last Amended**: 2026-08-29