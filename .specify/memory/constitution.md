# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Cross-layer dependencies MUST follow a strict unidirectional flow: Controller -> Service -> Repository -> Domain/Model. Configuration classes MUST be isolated and only injected where necessary.

### II. Spring Boot Convention and Idiomatic Usage
The project MUST leverage Spring Boot features and best practices. This includes, but is not limited to, auto-configuration, dependency injection, Spring Data JPA for data access, and Spring MVC for web handling. Custom configurations MUST be clearly defined and documented.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST focus on individual components, while integration tests MUST verify interactions between layers and external dependencies (e.g., database). Test coverage MUST be maintained at a high level, with specific targets defined in the Quality Gates section.

### IV. Data Access Abstraction
The Repository layer MUST abstract all data access logic. Direct database interactions from other layers (e.g., Controllers, Services) are FORBIDDEN. Spring Data JPA repositories are the standard for data persistence.

### V. Observability and Logging
All components MUST implement structured logging for critical events, errors, and informational messages. Logs MUST be sufficiently detailed to aid in debugging and monitoring. The `org.springframework.samples.petclinic.system` package provides examples of basic logging and error handling.

## Development Workflow and Quality Gates

### Code Review and Compliance
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the core principles, coding standards, and test coverage requirements. Automated checks (e.g., static analysis, test execution) MUST pass before a pull request can be merged.

### Testing Strategy
- **Unit Tests**: Mandatory for all new classes and methods. Aim for >80% code coverage for new code.
- **Integration Tests**: Mandatory for verifying inter-layer communication, repository interactions, and controller endpoints. Specific integration tests for database interactions (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`) MUST be maintained and passed.
- **End-to-End Tests**: While not explicitly defined as a separate category in the current structure, the existing integration tests serve this purpose for core functionalities.

### Deployment Policy
Deployment to production environments requires successful completion of all automated tests, a successful code review, and explicit approval from the lead architect or designated release manager. Rollback procedures MUST be documented and tested.

## Governance

This Constitution supersedes all other informal practices and guidelines within the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments MUST include a migration plan to ensure existing code and practices are updated accordingly. All pull requests and code reviews MUST explicitly verify compliance with this Constitution. Complexity introduced into the codebase MUST be justified and documented.

**Version**: 1.0.0 | **Ratified**: 2026-09-03 | **Last Amended**: 2026-09-03