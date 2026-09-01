# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Components MUST NOT cross layer boundaries in an unintended manner.

### II. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities where appropriate. Custom configurations MUST be clearly defined and documented, primarily within `src/main/java/org/springframework/samples/petclinic/system` or relevant module configurations.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and/or integration tests. Existing tests MUST pass. Integration tests MUST cover interactions between layers and external dependencies (e.g., database). The `src/test` directory MUST reflect a robust testing strategy.

### IV. JPA Entity and Repository Standards
All JPA entities MUST extend `BaseEntity` and `NamedEntity` where applicable, ensuring consistent ID generation and naming. Repository interfaces MUST extend `JpaRepository` or similar Spring Data interfaces for data access operations.

### V. RESTful Controller Design
Controllers MUST adhere to RESTful principles, utilizing appropriate HTTP methods and status codes. Request and response payloads SHOULD be well-defined, leveraging DTOs where necessary for clarity and separation of concerns.

## Additional Constraints

### Technology Stack
The project MUST be built using Java and Spring Boot. Dependencies are managed via Maven. The primary database is H2, with support for MySQL and PostgreSQL demonstrated in integration tests.

### Internationalization (i18n)
All user-facing strings MUST be internationalized and managed through properties files located in `src/main/resources`. The `I18nPropertiesSyncTest` MUST pass to ensure consistency across languages.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the project's core principles, coding standards, and test coverage.

### Quality Gates
Automated checks, including compilation, static analysis (if configured), and all tests (unit and integration), MUST pass before a pull request can be merged.

Governance
This constitution supersedes all other development practices for the saritha-atmuri-xoriant/spring-petclinic repository. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of the core development team. All existing code MUST be migrated to comply with amendments within a reasonable timeframe, as defined by the amendment proposal. All pull requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-01 | **Last Amended**: 2026-09-01