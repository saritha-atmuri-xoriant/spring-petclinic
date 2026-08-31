# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Enforcement
Every component MUST adhere to a strict layered architecture: Controller, Service, Repository, and Domain. Direct dependencies MUST only exist between adjacent layers (e.g., Controller can depend on Service, Service on Repository, Repository on Domain). Cross-layer dependencies are forbidden.

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components (controllers, services, repositories, models) with a minimum of 80% code coverage. Integration tests MUST verify interactions between layers and external systems (e.g., database).

### III. Spring Boot Convention Adherence
The project MUST leverage Spring Boot conventions for configuration, dependency injection, and auto-configuration. Custom configurations (e.g., `WebConfiguration.java`, `CacheConfiguration.java`) MUST be clearly documented and justified.

### IV. Domain Model Integrity
Domain entities (e.g., `Owner.java`, `Pet.java`, `Vet.java`) MUST be POJOs with minimal logic, primarily focused on data representation and validation. Business logic MUST reside in the Service layer. Entities MUST be annotated appropriately for persistence (JPA).

### V. Observability and Monitoring
All controllers and services MUST be instrumented for observability. This includes structured logging for key operations and error handling. Integration tests for database interactions (e.g., `MySqlIntegrationTests.java`, `PostgresIntegrationTests.java`) implicitly support this by verifying data persistence and retrieval.

## Additional Constraints

The project MUST use Java as the primary programming language and Spring Boot as the core framework. Database interactions MUST be managed through Spring Data JPA. The project is designed to be deployable within a containerized environment, as indicated by the presence of `k8s/` directory. Development environments can be facilitated using `.devcontainer/`.

## Development Workflow

All code changes MUST be submitted as Pull Requests (PRs). Each PR MUST include:
1.  Unit tests covering the changes.
2.  Integration tests where applicable.
3.  A clear description of the changes and the problem they solve.
4.  All PRs MUST be reviewed by at least one other team member.
5.  Automated checks (CI pipeline) MUST pass before merging. This includes compilation, static analysis, and all tests.

## Governance

This Constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this Constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendment MUST include a migration plan if it impacts existing code or processes. All Pull Requests and code reviews MUST verify compliance with these principles.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31