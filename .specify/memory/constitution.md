# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Components MUST NOT cross layer boundaries inappropriately (e.g., a Repository directly calling a Controller).

### II. Spring Boot Convention and Idioms
The project MUST leverage Spring Boot features and best practices. This includes using Spring Data JPA for repositories, Spring MVC for controllers, and standard Spring Boot auto-configuration where applicable. Custom configurations MUST be clearly defined and documented.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and/or integration tests. Unit tests MUST verify individual component logic, while integration tests MUST validate interactions between components and with external systems (e.g., database). Existing tests MUST be maintained and updated.

### IV. Data Integrity and Validation
All data entities (e.g., `Owner`, `Pet`, `Vet`) MUST adhere to defined validation constraints (e.g., `@NotNull`, `@NotEmpty`). Data persistence operations MUST be handled exclusively through the defined Repository interfaces.

### V. Observability and Debuggability
The application MUST be designed with observability in mind. While explicit logging configurations are not detailed in the provided snippets, the principle implies that logging should be structured and informative, aiding in debugging and monitoring.

## Additional Constraints

### Technology Stack
The project MUST utilize Java as the primary programming language, with Spring Boot as the core framework. JPA and Hibernate are expected for data persistence. Maven is the build tool.

### Development Environment
The `.devcontainer` directory suggests a preference for containerized development environments, promoting consistency across developer setups.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the core principles, coding standards, and test coverage requirements.

### Quality Gates
Successful execution of all unit and integration tests is a mandatory quality gate for merging code. Static analysis tools (if configured) should also pass without critical violations.

Governance
This constitution supersedes all other informal practices. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. A migration plan must be provided for any changes that impact existing code or workflows. All pull requests and code reviews must verify compliance with this constitution. Complexity must be justified with clear documentation.

**Version**: 1.0.0 | **Ratified**: 2026-08-30 | **Last Amended**: 2026-08-30