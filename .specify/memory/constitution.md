# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Components MUST NOT cross layer boundaries in an unintended manner. This ensures maintainability and separation of concerns.

### II. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities where appropriate. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be clearly defined and serve a specific purpose beyond default behavior.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components (e.g., `OwnerControllerTests`, `PetValidatorTests`), while integration tests (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`) MUST validate interactions between components and with external systems like databases.

### IV. Data Persistence Abstraction
The project MUST utilize Spring Data JPA for data access. Repository interfaces (e.g., `OwnerRepository`, `VetRepository`) MUST abstract the underlying persistence mechanism, allowing for easier testing and potential future database migrations.

### V. RESTful API Design
Controller classes (e.g., `OwnerController`, `PetController`) MUST adhere to RESTful principles for API design, utilizing standard HTTP methods and status codes for resource manipulation and retrieval.

## Additional Constraints

### Technology Stack
The project MUST be built using Java and Spring Boot. Dependencies are managed via Maven (implied by typical Spring Boot project structure). Database interactions are handled through Spring Data JPA.

### Development Environment
The presence of `.devcontainer/` suggests a preference for containerized development environments, promoting consistency across developer setups.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to these principles, code quality, and test coverage.

### Quality Gates
Automated checks, including compilation, static analysis (if configured), and all tests (unit and integration), MUST pass before a pull request can be merged.

Governance
This constitution supersedes all other informal development practices. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of the core development team. All existing code MUST be migrated to comply with any ratified amendments within a reasonable timeframe, to be defined per amendment.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02