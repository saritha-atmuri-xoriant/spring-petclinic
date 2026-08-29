# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Cross-layer dependencies MUST follow a strict top-down flow (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between unrelated layers are forbidden.

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal, well-documented, and only introduced when explicit deviation from convention is required and justified.

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed following a TDD approach. Unit tests MUST cover individual components, while integration tests MUST validate interactions between components and with external systems (e.g., database). The existing extensive test suite (17+ test files) MUST be maintained and expanded.

### IV. JPA and Spring Data Repository Best Practices
All data access MUST be performed through Spring Data JPA repositories. Repositories MUST be kept lean, focusing on CRUD operations and custom queries. Business logic MUST NOT be embedded within repositories. Entities (e.g., `Owner.java`, `Pet.java`, `Vet.java`) MUST adhere to JPA standards and validation constraints.

### V. Observability and Debuggability
The application MUST be designed with observability in mind. While explicit logging configurations are not detailed in the provided snippets, all controllers and services SHOULD emit structured logs. The use of Spring Boot Actuator or similar mechanisms for monitoring is encouraged.

## Additional Constraints

### Technology Stack
The project MUST primarily utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. Dependencies MUST be managed via Maven.

### Database Agnosticism (via Spring Data JPA)
While integration tests exist for MySQL and PostgreSQL, the core application logic SHOULD remain agnostic to the underlying database technology, relying on Spring Data JPA abstractions.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the core principles, coding standards, and test coverage.

### Quality Gates
Automated checks, including compilation, static analysis (e.g., SonarQube), and all unit/integration tests, MUST pass before a pull request can be merged.

Governance
This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. A migration plan MUST be provided for any significant changes. All pull requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-29 | **Last Amended**: 2026-08-29