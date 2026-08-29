# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Cross-layer dependencies MUST follow a strict top-down flow (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between unrelated layers (e.g., Controllers directly accessing Repositories) are forbidden.

### II. Spring Boot Conventions
The project MUST leverage Spring Boot's auto-configuration capabilities where appropriate. Configuration properties MUST be managed via `application.properties` or `application.yml`. Spring's dependency injection and component scanning MUST be used for managing beans and their lifecycles.

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed with accompanying unit and integration tests. Unit tests MUST focus on individual components in isolation, while integration tests MUST verify the interaction between components and with external systems (e.g., database). Test coverage MUST be maintained at a high level, with critical paths and business logic thoroughly validated. The presence of `src/test` directory with numerous tests for controllers, services, and models indicates this principle.

### IV. Data Persistence Abstraction
Data access MUST be performed exclusively through Spring Data repositories. Direct SQL queries or manual JDBC operations are prohibited. The repository layer MUST abstract the underlying data source implementation, allowing for easier swapping of persistence technologies if needed.

### V. RESTful API Design
Controllers MUST expose RESTful endpoints following standard HTTP methods (GET, POST, PUT, DELETE) and status codes. Data transfer between client and server MUST utilize JSON. The structure of controllers (e.g., `OwnerController`, `PetController`) indicates a clear separation of concerns for different resource types.

## Additional Constraints

The project MUST adhere to Java 17 or later.
The project MUST use Maven as the build tool.
The project MUST support multiple database integrations as evidenced by `MySqlIntegrationTests.java` and `PostgresIntegrationTests.java`.
Internationalization (i18n) MUST be implemented for all user-facing text, as indicated by `I18nPropertiesSyncTest.java` and `WebConfiguration.java`.

## Development Workflow

Code changes MUST be submitted via Pull Requests (PRs).
All PRs MUST undergo a code review by at least one other team member.
Automated checks, including compilation, static analysis, and unit/integration tests, MUST pass before a PR can be merged.
The `k8s/` directory suggests potential for containerized deployments, and any changes related to deployment configurations must be reviewed for compatibility.
The `.devcontainer/` directory indicates a standardized development environment, and adherence to its configuration is expected.

## Governance
This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this constitution require a formal proposal, review by all core contributors, and a documented migration plan if necessary. Compliance with this constitution will be verified during code reviews and automated checks.

**Version**: 1.0.0 | **Ratified**: 2026-08-29 | **Last Amended**: 2026-08-29