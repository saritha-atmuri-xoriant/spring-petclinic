# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Model, Configuration, Service, etc.). Components MUST NOT directly depend on components from layers lower than their immediate predecessor (e.g., Controllers MUST NOT directly call Repositories; they MUST go through Services).

### II. Spring Boot Conventions
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Configuration files (e.g., `application.properties`, `application.yml`) MUST be used for application-wide settings. Spring annotations (e.g., `@Controller`, `@Repository`, `@Service`, `@Configuration`) MUST be used to define component roles.

### III. Test Coverage and Quality Gates (NON-NEGOTIABLE)
All new features and bug fixes MUST include comprehensive unit and integration tests. Unit tests MUST cover individual component logic, while integration tests MUST verify interactions between components and with external systems (like databases). A minimum test coverage threshold (e.g., 80%) MUST be maintained for all production code. All tests MUST pass before code can be merged.

### IV. Data Persistence Abstraction
Data access logic MUST be encapsulated within Repository interfaces (e.g., `OwnerRepository`, `VetRepository`), leveraging Spring Data JPA. Domain entities (e.g., `Owner`, `Pet`, `Vet`) MUST be mapped to database tables using JPA annotations. Direct SQL queries within controllers or services are prohibited, except for highly specialized, performance-critical scenarios with explicit architectural approval.

### V. Observability and Logging
All significant application events, errors, and request flows MUST be logged using a structured logging framework (e.g., SLF4j with Logback). Log messages MUST be informative and actionable. The project MUST include mechanisms for monitoring application health and performance, potentially through Spring Boot Actuator or similar tools.

## Development Workflow

The standard development workflow involves:
1.  **Feature Branching**: Create a new branch for each feature or bug fix.
2.  **Development**: Implement the feature, adhering to the core principles. Write unit and integration tests concurrently.
3.  **Local Testing**: Run all tests locally to ensure correctness and coverage.
4.  **Code Review**: Submit a Pull Request (PR) for review by at least one other team member. The PR MUST include a clear description of changes and rationale. Reviewers MUST verify adherence to this constitution.
5.  **CI/CD Pipeline**: Upon merging to the main branch, the CI/CD pipeline will automatically build, test, and deploy the application.

## Governance

This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this constitution require a formal proposal, a documented justification, and approval from at least two-thirds of the core development team. Any approved amendments MUST include a migration plan for existing code and documentation updates. All Pull Requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-01 | **Last Amended**: 2026-09-01