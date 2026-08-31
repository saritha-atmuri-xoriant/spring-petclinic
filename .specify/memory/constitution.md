# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Components MUST NOT cross layer boundaries in an unintended manner.

### II. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities where applicable. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be clearly documented and justified.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and/or integration tests. Existing tests MUST pass. Integration tests MUST cover critical paths and inter-layer interactions, as evidenced by files like `OwnerControllerTests.java`, `ClinicServiceTests.java`, and database integration tests (`MySqlIntegrationTests.java`, `PostgresIntegrationTests.java`).

### IV. Data Persistence Abstraction
The project MUST utilize Spring Data JPA for data access. Repository interfaces MUST abstract persistence concerns, as demonstrated by `OwnerRepository.java`, `PetTypeRepository.java`, and `VetRepository.java`.

### V. RESTful API Design
Controller classes (e.g., `OwnerController.java`, `PetController.java`) MUST adhere to RESTful principles for API design, utilizing standard HTTP methods and status codes.

## Development Workflow

The standard development workflow involves:
1. **Feature/Bug Fix Identification**: Clearly define the scope of the change.
2. **Branching**: Create a new feature branch from the main development branch.
3. **Development**: Implement the change, adhering to the Core Principles. Write unit and integration tests.
4. **Local Testing**: Run all tests to ensure no regressions.
5. **Code Review**: Submit a Pull Request (PR) for review by at least one other team member. The PR MUST include a clear description of the changes and link to any relevant issue.
6. **CI/CD Pipeline**: Upon merging to the main branch, the CI/CD pipeline will automatically build, test, and deploy the application.

## Governance
This constitution supersedes all other informal development practices. Amendments to this constitution require a formal proposal, review by the core development team, and a majority approval. Any approved amendments MUST be documented, including the rationale for the change and a plan for migrating existing code or practices if necessary. All Pull Requests and code reviews MUST verify compliance with this constitution. Complexity MUST be justified with clear documentation.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31