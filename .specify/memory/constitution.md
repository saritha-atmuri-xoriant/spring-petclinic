# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Service, Model, Configuration, etc.). Components MUST NOT directly depend on components from layers lower than their immediate predecessor (e.g., Controllers MUST NOT directly call Repositories).

### II. Spring Boot Convention and Configuration
The project MUST leverage Spring Boot conventions for auto-configuration and dependency management. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be clearly defined and adhere to Spring's configuration patterns.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and/or integration tests. Existing functionality MUST maintain a high level of test coverage, as evidenced by the numerous test files present in the `src/test` directory. Integration tests MUST specifically cover interactions between layers and external dependencies (e.g., database access).

### IV. Domain Model Integrity
The domain model classes (e.g., `Owner`, `Pet`, `Vet`) MUST be the single source of truth for data structures. All business logic related to these entities SHOULD be encapsulated within their respective classes or associated service layers. Validation rules defined in the model (e.g., `@NotNull`) MUST be respected throughout the application.

### V. Observability and Debuggability
The application MUST be designed with observability in mind. While explicit logging configurations are not detailed in the provided snippets, the presence of `CrashController` and various test suites suggests a focus on identifying and debugging issues. Future enhancements should consider structured logging and tracing.

## Development Workflow and Quality Gates

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the core principles outlined in this constitution, including architectural layering, test coverage, and adherence to Spring Boot conventions.

### Testing Gates
Automated tests (unit and integration) MUST pass successfully in the CI pipeline before any code can be merged. Integration tests specifically targeting database interactions (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`) are critical for ensuring data persistence and retrieval integrity.

### Deployment Readiness
Code deployed to production environments MUST have passed all automated tests, undergone successful code reviews, and have been validated through integration testing against representative environments.

## Governance

This constitution supersedes all other informal development practices. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All pull requests and code reviews MUST explicitly verify compliance with this constitution. Complexity introduced into the codebase MUST be justified and documented.

**Version**: 1.0.0 | **Ratified**: 2026-08-30 | **Last Amended**: 2026-08-30