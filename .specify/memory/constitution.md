# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, or Test). Cross-layer dependencies MUST follow a strict top-down flow (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between unrelated layers (e.g., Controllers directly accessing Repositories) are forbidden.

### II. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal and clearly justified, adhering to established Spring patterns. Dependencies MUST be managed via Spring's dependency injection and component scanning.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components (e.g., `OwnerControllerTests.java`, `PetValidatorTests.java`), while integration tests (e.g., `MySqlIntegrationTests.java`, `PetClinicIntegrationTests.java`) MUST validate interactions between components and with external systems like databases. Test coverage MUST be tracked and maintained.

### IV. Domain Model Integrity
Domain entities (e.g., `Owner.java`, `Pet.java`, `Vet.java`) MUST be POJOs with clear responsibilities. Persistence logic MUST be encapsulated within Repository interfaces (e.g., `OwnerRepository.java`). Validation rules MUST be applied at the domain or controller layer using standard Java Bean Validation annotations and custom validators (`PetValidator.java`).

### V. Observability and Configuration Management
Application configuration MUST be externalized and managed through Spring Boot's configuration properties. Logging MUST be structured and informative, aiding in debugging and monitoring. The `CacheConfiguration.java` demonstrates explicit configuration for caching, which is a form of observability and performance tuning.

## Development Workflow

The standard development workflow involves:
1. **Feature/Bug Identification**: Clearly define the scope of the change.
2. **Branching**: Create a new feature branch from the main development branch.
3. **Development**: Implement the change, adhering to the Core Principles. Write unit and integration tests concurrently.
4. **Code Review**: Submit a Pull Request (PR) for review by at least one other team member. The PR MUST include a description of the changes and how they were tested.
5. **Testing**: All automated tests MUST pass in the CI pipeline. Manual testing may be required for critical path changes.
6. **Merging**: Once approved and tests pass, the PR can be merged into the main development branch.

## Governance

This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this constitution require a formal proposal, a documented justification for the change, and approval by a majority of the core development team. Any approved amendments must include a migration plan if existing code or practices need to be updated to comply with the new rules. All Pull Requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31