# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Cross-layer dependencies MUST follow a strict top-down flow (Controller -> Service -> Repository -> Domain/Model), with Configuration and Test layers being exceptions for dependency injection and testing utilities respectively.

### II. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal and clearly justified, adhering to established Spring patterns.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and/or integration tests. Unit tests MUST target individual components, while integration tests MUST verify interactions between layers and external systems (e.g., database interactions via `MySqlIntegrationTests.java`, `PostgresIntegrationTests.java`). Test coverage MUST be maintained above 80%.

### IV. Domain Entity Integrity
Domain entities (e.g., `Owner.java`, `Pet.java`, `Vet.java`) MUST be POJOs with appropriate JPA annotations for persistence and validation annotations for data integrity. They MUST NOT contain business logic beyond basic getters, setters, and validation-related methods.

### V. Observability and Logging
All controllers and services MUST implement structured logging for request handling, errors, and key business events. The `PetClinicApplication.java` and related configurations SHOULD be instrumented for monitoring.

## Development Workflow

### Code Review and Quality Gates
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the core principles, code style, and test coverage. Automated checks, including static analysis and unit tests, MUST pass before merging.

### Database Interaction Standards
Repository interfaces (e.g., `OwnerRepository.java`) MUST be used for all data access operations. Direct SQL queries within controllers or services are forbidden. Integration tests MUST validate database schema and data integrity.

### Internationalization (i18n) Compliance
All user-facing strings MUST be externalized and managed through properties files (e.g., `messages.properties`). The `I18nPropertiesSyncTest.java` MUST pass to ensure all strings are translated across all supported locales.

## Governance
This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this constitution require a formal proposal, a documented justification, and approval by a majority of the core development team. Any amendments MUST include a plan for migrating existing code to comply with the new rules. All pull requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31