# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT directly call Repositories).

### II. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities where appropriate. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be clearly documented and justified.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components, while integration tests MUST verify interactions between components and layers, including database interactions (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`). Test coverage MUST be maintained above 80%.

### IV. JPA Repository Pattern Enforcement
Data access MUST be exclusively handled through Spring Data JPA repositories. Custom repository implementations are discouraged unless absolutely necessary and must be explicitly approved.

### V. RESTful API Design
Controller layer components (e.g., `OwnerController`, `PetController`) MUST adhere to RESTful principles for API design, utilizing standard HTTP methods and status codes.

## Additional Constraints

### Technology Stack
The project MUST utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. External dependencies MUST be managed via Maven.

### Database Agnosticism (via Integration Tests)
While specific integration tests exist for MySQL and PostgreSQL, the core application logic SHOULD remain agnostic to the underlying database. Configuration for different databases should be managed externally.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the core principles, coding standards, and test coverage requirements.

### Quality Gates
Automated checks, including static analysis, unit tests, and integration tests, MUST pass before a pull request can be merged. Continuous Integration (CI) pipelines MUST enforce these gates.

## Governance
This Constitution supersedes all other development practices for the saritha-atmuri-xoriant/spring-petclinic repository. Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code to comply with the new rules. All pull requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-30 | **Last Amended**: 2026-08-30