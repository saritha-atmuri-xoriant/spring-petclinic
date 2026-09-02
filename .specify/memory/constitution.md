# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories).

### II. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be minimal and clearly justified, adhering to Spring's idiomatic patterns.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components, while integration tests MUST verify interactions between layers and external dependencies (e.g., database, external services). Existing tests MUST be maintained and expanded.

### IV. Data Access Abstraction
Data access logic MUST be encapsulated within Repository interfaces (e.g., `OwnerRepository`, `VetRepository`), leveraging Spring Data JPA. Direct database manipulation from controllers or service layers is FORBIDDEN.

### V. Domain Model Integrity
Domain entities (e.g., `Owner`, `Pet`, `Vet`) MUST be POJOs with appropriate JPA annotations and validation constraints. They MUST NOT contain business logic that belongs in the service layer.

## Development Workflow and Quality Gates

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to architectural principles, coding standards, and test coverage requirements.

### Testing Gates
Automated tests (unit and integration) MUST pass successfully in the CI pipeline before any pull request can be merged. Integration tests specifically targeting database interactions (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`) are critical for ensuring data persistence and retrieval correctness.

### Dependency Management
All external dependencies MUST be managed via Maven. New dependencies MUST be carefully evaluated for necessity and potential impact on the project's stability and security.

## Governance
This Constitution supersedes all other development practices for the saritha-atmuri-xoriant/spring-petclinic repository. Amendments to this Constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a migration plan to ensure existing code and practices are brought into compliance. All pull requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02