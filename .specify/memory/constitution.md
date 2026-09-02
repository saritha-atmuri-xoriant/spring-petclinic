# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Cross-layer dependencies MUST be strictly unidirectional, flowing downwards (e.g., Controllers depend on Services, Services depend on Repositories).

### II. Spring Boot Conventions
The project MUST leverage Spring Boot's auto-configuration capabilities and follow established Spring conventions for dependency injection, component scanning, and configuration management. Externalized configuration MUST be managed via `application.properties` or `application.yml`.

### III. Test-Driven Development (TDD) & Comprehensive Testing
All new features and bug fixes MUST be developed with a test-first approach. Unit tests MUST cover individual components, integration tests MUST verify interactions between components and with external systems (e.g., databases), and end-to-end tests (where applicable) MUST validate user flows. Test coverage MUST be maintained at a high level, with a minimum of 80% for critical business logic.

### IV. Domain-Driven Design Principles
The core domain entities (Owner, Pet, Vet, Visit, PetType, Specialty) MUST accurately represent the business concepts. Business logic MUST be encapsulated within the domain layer or service layer, not within controllers or repositories.

### V. Observability and Configuration
Application behavior MUST be configurable through external properties. Logging MUST be structured and informative, aiding in debugging and monitoring. Internationalization (i18n) MUST be handled consistently using Spring's i18n mechanisms.

## Additional Constraints

The project MUST utilize Java as the primary programming language and Spring Boot as the core framework. JPA and Hibernate MUST be used for data persistence. The project is designed to be deployable within a containerized environment (e.g., Docker, Kubernetes), as indicated by the presence of a `k8s` directory.

## Development Workflow

All code changes MUST be submitted as Pull Requests (PRs). Each PR MUST include comprehensive unit and integration tests. Code reviews are mandatory, with at least one reviewer approving the changes. Automated checks, including static analysis and test execution, MUST pass before merging.

## Governance

This Constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments must include a migration plan to ensure existing code adheres to the new principles. All Pull Requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02