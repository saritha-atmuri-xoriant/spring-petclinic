# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Direct dependencies MUST only flow downwards (e.g., Controllers depend on Services, Services depend on Repositories). No cross-layer dependencies are permitted except for those explicitly defined by framework conventions.

### II. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations MUST be minimal and clearly justified, documented within their respective classes (e.g., `WebConfiguration.java`, `CacheConfiguration.java`).

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and/or integration tests. Existing tests MUST be maintained and updated. Integration tests MUST cover critical paths, data access operations, and inter-component communication. Test files are clearly identifiable in the `src/test` directory.

### IV. Domain Model Integrity
Domain entities (e.g., `Owner.java`, `Pet.java`, `Vet.java`) MUST be POJOs with clear responsibilities. They MUST adhere to JPA entity conventions and utilize validation annotations where appropriate. Relationships between entities MUST be explicitly defined.

### V. Observability and Internationalization
The application MUST support internationalization (i18n) for user-facing messages, as evidenced by `I18nPropertiesSyncTest.java` and `WebConfiguration.java`. Logging and error handling SHOULD be structured to facilitate debugging and monitoring.

## Additional Constraints

The project MUST utilize Java as the primary programming language and Spring Boot as the core framework. Dependencies MUST be managed via Maven. Database interactions MUST be handled through Spring Data JPA repositories.

## Development Workflow

All code changes MUST be submitted via Pull Requests. Each Pull Request MUST include a description of the changes and be reviewed by at least one other team member. Automated checks, including compilation, testing, and static analysis (if configured), MUST pass before merging.

## Governance

This Constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. All Pull Requests and code reviews MUST verify compliance with these principles.

**Version**: 1.0.0 | **Ratified**: 2026-08-29 | **Last Amended**: 2026-08-29