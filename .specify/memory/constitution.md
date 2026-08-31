# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Direct dependencies MUST only flow downwards (e.g., Controller can depend on Service, but Service cannot depend on Controller).

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be minimal and clearly justified, adhering to established Spring patterns.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components (controllers, services, models), and integration tests MUST verify interactions between layers and with external dependencies (e.g., database, external APIs if any). Existing tests MUST be maintained and updated.

### IV. JPA Repository Abstraction
All data access MUST be performed through Spring Data JPA repositories. Custom repository implementations are discouraged unless absolutely necessary and clearly documented.

### V. RESTful API Design
Controllers MUST expose RESTful endpoints following standard HTTP methods and status codes. The API design SHOULD prioritize clarity, consistency, and ease of use for consumers.

## Additional Constraints

### Technology Stack
The project MUST utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. External dependencies MUST be managed via Maven.

### Database Agnosticism
While integration tests may target specific databases (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`), the core application logic MUST remain agnostic to the underlying database technology.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to architectural principles, coding standards, and test coverage.

### Quality Gates
Automated checks, including static analysis, unit tests, and integration tests, MUST pass successfully before a pull request can be merged.

Governance
This constitution supersedes all other development practices for the saritha-atmuri-xoriant/spring-petclinic repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. All existing code MUST be migrated to comply with amendments within a reasonable timeframe, to be defined per amendment. All pull requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31