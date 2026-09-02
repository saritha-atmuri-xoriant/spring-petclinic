# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Direct dependencies MUST only flow downwards (e.g., Controller can depend on Service, Service on Repository, but not vice-versa). This ensures maintainability and clear separation of concerns.

### II. Spring Boot Convention and Best Practices
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Configuration MUST be managed via `@Configuration` classes and properties. Dependency Injection MUST be used extensively for component wiring.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST target individual components (controllers, services, repositories) in isolation. Integration tests MUST verify the interaction between components and with external systems (e.g., database). Test coverage MUST be maintained at a high level, with critical paths having near-complete coverage.

### IV. Data Persistence Abstraction
Data access MUST be managed through Spring Data JPA repositories. Entities MUST be clearly defined with appropriate JPA annotations. Business logic MUST NOT contain direct SQL queries or low-level database interactions.

### V. Observability and Error Handling
All controllers and services MUST log relevant information for debugging and monitoring. Exceptions MUST be handled gracefully, with specific exceptions being caught and re-thrown or translated where appropriate. The `CrashController` serves as an example of explicit error simulation for testing.

## Development Workflow and Quality Gates

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the core principles, coding standards, and test coverage requirements.

### Testing Gates
Automated tests (unit and integration) MUST pass successfully in the CI pipeline before a pull request can be merged. Any failure in the test suite MUST block the merge.

### Deployment Policy
Deployments to production environments MUST be preceded by successful staging deployments and a final sign-off from the lead architect or designated release manager. Rollback procedures MUST be documented and tested.

## Governance
This constitution supersedes all other development practices for the saritha-atmuri-xoriant/spring-petclinic repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code to comply with the new rules. All pull requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02