# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Cross-layer dependencies MUST follow a strict top-down flow (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between unrelated layers (e.g., Controllers directly accessing Repositories) are forbidden.

### II. Spring Boot Convention and Configuration
The project MUST leverage Spring Boot conventions for auto-configuration and dependency injection. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be clearly defined and adhere to Spring's configuration best practices. Externalized configuration (e.g., `application.properties`) MUST be used for environment-specific settings.

### III. Test Coverage and Integration
Comprehensive unit tests MUST be provided for all business logic and controller components. Integration tests (e.g., `OwnerControllerTests.java`, `ClinicServiceTests.java`, `MySqlIntegrationTests.java`) MUST verify the interaction between different layers and external dependencies like databases. All new features or significant changes MUST include corresponding unit and integration tests.

### IV. Domain Model Integrity
Domain entities (e.g., `Owner.java`, `Pet.java`, `Vet.java`) MUST be POJOs with clear responsibilities. They MUST utilize Jakarta Persistence annotations for ORM mapping and Jakarta Bean Validation annotations for data integrity. Relationships between entities MUST be explicitly defined and managed.

### V. Observability and Logging
Application behavior and potential issues MUST be observable through structured logging. All significant events, errors, and request flows MUST be logged using appropriate log levels. The `PetClinicApplication.java` and associated configurations SHOULD be reviewed for any existing logging or observability patterns.

## Development Workflow

### Code Review and Quality Gates
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the core principles, code quality, test coverage, and documentation. Automated checks, including static analysis and unit/integration tests, MUST pass before a pull request can be merged.

### Versioning and Breaking Changes
The project follows Semantic Versioning (MAJOR.MINOR.PATCH). Breaking changes MUST be clearly documented in the release notes and require a MAJOR version increment. All dependencies MUST be managed and kept up-to-date to mitigate security vulnerabilities and leverage new features.

## Governance
This Constitution supersedes all other informal development practices. Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All pull requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-01 | **Last Amended**: 2026-09-01