# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Enforcement
Every component MUST adhere to a strict layered architecture: Controller, Service, Repository, and Domain/Model. Direct dependencies MUST only flow downwards (e.g., Controller can depend on Service, but Service cannot depend on Controller). This ensures separation of concerns and maintainability.

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components (controllers, services, repositories, models), and integration tests MUST verify interactions between layers and with external systems (like databases). A minimum of 80% code coverage MUST be maintained for production-ready code.

### III. Spring Boot Convention Adherence
The project MUST leverage Spring Boot conventions for configuration, dependency injection, and auto-configuration. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be clearly documented and justified. Avoid unnecessary boilerplate code by utilizing Spring Boot's opinionated defaults.

### IV. Data Persistence Abstraction
Data access MUST be managed through Spring Data JPA repositories. The repository layer MUST abstract away the underlying database implementation details. Integration tests for different database types (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`) MUST be maintained to ensure portability.

### V. RESTful API Design
Controllers MUST expose RESTful APIs following standard HTTP methods and status codes. Input validation MUST be performed at the controller or service layer using appropriate annotations and validators (e.g., `PetValidator`).

## Development Workflow

The development workflow for the Spring Petclinic project is as follows:

1.  **Feature Branching**: All new development MUST occur on dedicated feature branches.
2.  **Code Implementation**: Implement the feature, adhering to the core principles.
3.  **Unit Testing**: Write comprehensive unit tests for all new code.
4.  **Integration Testing**: Develop integration tests to verify cross-layer interactions.
5.  **Code Review**: Submit a Pull Request (PR) for review by at least one other team member. The PR MUST include a clear description of changes and rationale.
6.  **CI/CD Pipeline**: Upon merging to the main branch, the CI/CD pipeline will automatically build, test, and deploy the application.

## Governance

This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Any proposed amendments to this constitution MUST be submitted as a formal proposal, clearly outlining the rationale, impact, and migration plan. Amendments require a majority vote of the core development team and MUST be documented with an updated version and amendment date. All Pull Requests and code reviews MUST verify compliance with these principles.

**Version**: 1.0.0 | **Ratified**: 2026-09-04 | **Last Amended**: 2026-09-04