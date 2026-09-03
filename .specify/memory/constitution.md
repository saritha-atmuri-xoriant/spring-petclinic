# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Enforcement
Every component MUST adhere to a strict layered architecture: Controller, Service, Repository, and Domain. Dependencies MUST flow downwards (e.g., Controllers depend on Services, Services depend on Repositories, Repositories depend on Domain models). Direct dependencies between non-adjacent layers are forbidden.

### II. Test Coverage Mandate
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST cover individual components (controllers, services, repositories) in isolation. Integration tests MUST verify the interaction between layers and with external dependencies (e.g., database). A minimum of 80% code coverage for new code is required.

### III. Spring Boot Convention Adherence
The project MUST leverage Spring Boot conventions for configuration, dependency injection, and auto-configuration. Custom configurations SHOULD be minimized and clearly documented. Externalized configuration (e.g., `application.properties`, environment variables) MUST be preferred over hardcoded values.

### IV. RESTful API Design
Controllers MUST expose RESTful APIs following standard HTTP methods (GET, POST, PUT, DELETE) and status codes. Data transfer SHOULD utilize JSON. APIs MUST be versioned if significant changes are introduced.

### V. Database Interaction via Repositories
All data persistence and retrieval operations MUST be performed exclusively through Spring Data JPA repositories. Direct SQL queries or JDBC calls within service or controller layers are prohibited.

## Additional Constraints

The project MUST use Java as the primary programming language.
The project MUST be built using Maven.
The project MUST be compatible with recent stable versions of Spring Boot and Jakarta EE.
The project MUST support multiple database integrations (e.g., H2, MySQL, PostgreSQL) as demonstrated by existing integration tests.

## Development Workflow

Code changes MUST be submitted as Pull Requests (PRs).
All PRs MUST undergo a thorough code review by at least one other team member.
Automated checks (CI pipeline) MUST pass before a PR can be merged. These checks include compilation, unit tests, integration tests, and static code analysis.
The project utilizes a feature branch workflow. Developers should create branches for new features or bug fixes and merge them back into the main branch after review and approval.

## Governance

This Constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository.
Amendments to this Constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments must include a migration plan if existing code or practices need to be updated.
All Pull Requests and code reviews MUST verify compliance with the principles outlined in this Constitution.
Complexity in the codebase MUST be justified with clear documentation and robust testing.

**Version**: 1.0.0 | **Ratified**: 2026-09-03 | **Last Amended**: 2026-09-03