# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Cross-layer dependencies MUST follow a strict top-down flow (Controller -> Service -> Repository -> Domain/Model), with Configuration and Test layers being exceptions that can be injected where needed.

### II. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal and clearly justified, adhering to established Spring patterns.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components (controllers, services, repositories, models), while integration tests MUST validate interactions between components and with external systems (e.g., database, external APIs if any). Test coverage MUST be tracked and maintained.

### IV. Domain-Driven Design Principles
The core domain entities (`Owner`, `Pet`, `Vet`, `Visit`, `PetType`, `Specialty`) MUST be the central focus. Business logic SHOULD be encapsulated within these domain objects or dedicated service classes, minimizing anemic domain models.

### V. Observability and Logging
All critical operations and error conditions MUST be logged using structured logging. The application MUST provide mechanisms for monitoring its health and performance, particularly in production environments.

## Additional Constraints

### Database Agnosticism
While integration tests demonstrate support for MySQL and PostgreSQL, the core application logic MUST remain agnostic to the specific database implementation. Data access MUST be abstracted through Spring Data repositories.

### Internationalization (i18n)
All user-facing strings MUST be externalized and managed through properties files, as enforced by `I18nPropertiesSyncTest.java`. Translations MUST be complete for all supported locales.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to this constitution, code quality, test coverage, and architectural principles.

### Continuous Integration
The project MUST integrate with a CI/CD pipeline that automatically builds, tests, and analyzes the code on every commit. Build failures MUST halt the pipeline and prevent merging.

### Dependency Management
Dependencies MUST be managed via Maven. Updates to dependencies MUST be carefully considered, tested, and documented.

## Governance
This constitution supersedes all other development practices for the saritha-atmuri-xoriant/spring-petclinic repository. Amendments to this constitution require a formal proposal, documented justification, and approval by the project lead. Any approved amendments MUST include a migration plan to bring existing code into compliance. All pull requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31