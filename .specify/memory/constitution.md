# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Components MUST NOT cross layer boundaries inappropriately (e.g., a Controller directly calling a Repository).

### II. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be minimal and clearly justified, adhering to established Spring patterns.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and/or integration tests. Existing tests MUST pass. Integration tests MUST specifically cover inter-layer communication and critical business logic flows. The presence of numerous integration tests (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`) indicates a strong emphasis on this principle.

### IV. Domain Model Integrity
Domain entities (e.g., `Owner`, `Pet`, `Vet`) MUST be defined with appropriate JPA annotations and validation constraints. Relationships between entities MUST be clearly defined and managed.

### V. Observability and Configuration Management
The application MUST support standard Spring Boot Actuator endpoints for monitoring. Configuration properties MUST be managed externally (e.g., `application.properties`, environment variables) and not hardcoded within the codebase.

## Additional Constraints

### Technology Stack
The project MUST utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. Database interactions are expected to be managed via JPA repositories.

### Internationalization (i18n)
All user-facing strings MUST be internationalized and managed through properties files. The `I18nPropertiesSyncTest` mandates that all strings are translated across all supported locales.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the principles outlined in this constitution, code quality, and test coverage.

### Testing Gates
Successful execution of all unit and integration tests is a mandatory gate for merging code. CI/CD pipelines MUST enforce this requirement.

## Governance
This constitution supersedes all other development practices for the saritha-atmuri-xoriant/spring-petclinic repository. Amendments to this constitution require a formal proposal, documented justification, and approval by the project lead. All amendments MUST include a plan for migrating existing code to comply with the changes. All pull requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31