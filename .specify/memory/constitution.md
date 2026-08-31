# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain, Configuration, Test). Direct dependencies MUST only flow downwards (e.g., Controller can depend on Service, Service on Repository, but not vice-versa). This ensures maintainability and clear separation of concerns.

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal, well-documented, and only introduced when standard conventions are insufficient or require explicit customization for performance or specific feature needs.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components (e.g., `OwnerControllerTests.java`, `PetValidatorTests.java`), while integration tests (e.g., `MySqlIntegrationTests.java`, `PetClinicIntegrationTests.java`) MUST validate interactions between components and with the data layer. Test coverage metrics MUST be maintained and reviewed.

### IV. Domain Model Integrity
The domain model classes (e.g., `Owner.java`, `Pet.java`, `Vet.java`) MUST be the single source of truth for business entities. They MUST be designed for immutability where appropriate and enforce business rules through validation annotations and encapsulated logic. Persistence concerns (JPA annotations) MUST be confined to these entities and their associated repositories.

### V. Observability and Diagnostics
The application MUST be instrumented for observability. This includes structured logging (as implied by Spring Boot's default logging configuration) and the presence of specific diagnostic controllers like `CrashController.java` to aid in debugging production issues.

## Additional Constraints

The project MUST adhere to the following constraints:
*   **Technology Stack**: Primarily Java, Spring Boot, Spring Data JPA, Thymeleaf for templating.
*   **Database**: Support for multiple database integrations as evidenced by `MySqlIntegrationTests.java` and `PostgresIntegrationTests.java`. Configuration for these should be externalized.
*   **Internationalization**: All user-facing strings MUST be internationalized using Spring's message source mechanism, as enforced by `I18nPropertiesSyncTest.java`.

## Development Workflow

*   **Branching Strategy**: Feature branches MUST be created from the main development branch.
*   **Code Reviews**: All pull requests MUST undergo at least one thorough code review by a team member familiar with the project's architecture and principles. Reviews MUST verify adherence to this constitution.
*   **Testing Gates**: CI/CD pipelines MUST include automated execution of all unit and integration tests. Builds MUST fail if tests do not pass.
*   **Deployment**: Deployments to production environments MUST be preceded by successful integration tests against a staging environment that mirrors production.

## Governance

This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a migration plan to ensure existing code and practices are brought into compliance. All pull requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31