# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Enforcement
Every new feature or modification MUST adhere to the established layered architecture: Controller, Service, Repository, and Domain/Model. Direct dependencies between non-adjacent layers are forbidden (e.g., Controller directly calling Repository). This ensures separation of concerns and maintainability.

### II. Test Coverage Mandate
All new code MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components (e.g., controllers, services, models) in isolation. Integration tests MUST verify the interaction between components and with external systems (e.g., database, external APIs). A minimum of 80% code coverage for new code is required.

### III. Spring Boot Convention Adherence
The project MUST leverage Spring Boot conventions for configuration, dependency injection, and auto-configuration. Custom configurations (e.g., `WebConfiguration.java`, `CacheConfiguration.java`) MUST be clearly documented and follow Spring best practices.

### IV. Data Persistence Integrity
All data persistence operations MUST be handled exclusively through the Repository layer. Direct manipulation of database connections or SQL queries outside of repository interfaces is forbidden. Data validation MUST be implemented at the appropriate layers (e.g., using Jakarta Bean Validation annotations in models and controllers).

### V. Observability and Logging
All significant operations, errors, and state changes MUST be logged using structured logging. The project MUST utilize Spring Boot's Actuator or equivalent for health checks and metrics.

## Additional Constraints

The project MUST utilize Java as the primary programming language and Spring Boot as the core framework. Dependencies MUST be managed via Maven. The project is intended to be deployed as a web application, and therefore, web-related best practices (e.g., RESTful API design, proper HTTP status codes) MUST be followed. Containerization configurations (e.g., `k8s/` directory) indicate an intent for containerized deployment, and new features should consider this.

## Development Workflow

All code changes MUST be submitted via Pull Requests (PRs). Each PR MUST be reviewed by at least one other team member. Automated checks, including static analysis, unit tests, and integration tests, MUST pass before a PR can be merged. Code reviews MUST verify adherence to the core principles and overall code quality.

## Governance

This Constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this Constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments must include a migration plan for existing code if necessary. All Pull Requests and code reviews must explicitly verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31