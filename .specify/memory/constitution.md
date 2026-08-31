# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Enforcement
Every component MUST adhere to a strict layered architecture: Controller, Service, Repository, and Domain/Model. Dependencies MUST flow downwards (Controller -> Service -> Repository -> Domain). Direct dependencies between non-adjacent layers are prohibited.

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components (e.g., controllers, services, repositories) in isolation. Integration tests MUST verify the interaction between layers and with external systems (e.g., database, external APIs). A minimum of 80% code coverage MUST be maintained for all new code.

### III. Spring Boot Convention Adherence
The project MUST leverage Spring Boot conventions for configuration, dependency injection, and auto-configuration. Custom configurations SHOULD be minimal and clearly justified. All beans MUST be explicitly defined or auto-configured by Spring Boot.

### IV. RESTful API Design
Controllers MUST expose RESTful APIs following standard HTTP methods (GET, POST, PUT, DELETE) and status codes. APIs SHOULD be stateless and use JSON for request and response bodies.

### V. Data Persistence Abstraction
Data access MUST be managed through Spring Data repositories. Direct SQL queries within service or controller layers are prohibited. All database interactions MUST be abstracted by repository interfaces.

## Additional Constraints

The project MUST use Java as the primary programming language.
The project MUST use Maven as the build tool.
The project MUST use JUnit 5 for unit and integration testing.
The project MUST use Spring Boot for application framework.
The project MUST use Spring Data JPA for data persistence.
The project MUST use a relational database (e.g., H2, PostgreSQL, MySQL) for data storage.
The project MUST adhere to Java Bean Validation (JSR 380) for data validation.
The project MUST implement internationalization (i18n) for all user-facing strings.

## Development Workflow

All code changes MUST be submitted as Pull Requests (PRs).
Each PR MUST be reviewed by at least one other team member.
All automated tests (unit, integration) MUST pass before a PR can be merged.
Code reviews MUST verify adherence to the core principles and architectural guidelines.
New features or significant changes MUST include updated or new documentation.
The `k8s/` directory contains Kubernetes deployment configurations. These should be kept up-to-date with application changes.
The `.devcontainer/` directory provides development environment configurations, ensuring consistency across developer machines.

## Governance

This Constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository.
Amendments to this Constitution require a formal proposal, documented justification, and approval by a majority of the core development team.
Any approved amendment MUST include a migration plan to ensure existing code and processes comply with the new rules.
All Pull Requests and code reviews MUST verify compliance with this Constitution.
Complexity in the codebase MUST be justified and documented.
The `src/test/java` directory contains the primary source of truth for testing conventions.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31