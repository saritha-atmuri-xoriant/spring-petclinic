# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Components MUST NOT cross layer boundaries in an unintended manner.

### II. Spring Boot Conventions
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Configuration MUST be managed via `application.properties` or `@Configuration` classes. Dependency Injection MUST be managed by Spring.

### III. Test Coverage (NON-NEGOTIABLE)
All new features and significant bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST focus on individual component logic, while integration tests MUST verify interactions between components and layers, including database persistence and API endpoints. Existing tests MUST be maintained and updated.

### IV. Data Persistence Integrity
All data persistence operations MUST be handled exclusively by the Repository layer, utilizing Spring Data JPA. Domain entities MUST be properly annotated for persistence. Data access logic SHOULD NOT be duplicated across different layers.

### V. RESTful API Design
Controller layer components MUST expose RESTful endpoints following standard HTTP methods and status codes. Request and response payloads SHOULD be well-defined and consistent.

## Additional Constraints

**Technology Stack**: The project MUST utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. Database interactions are expected to be with a relational database (e.g., MySQL, PostgreSQL, H2).

**Containerization**: The project MUST be containerizable, with considerations for Docker and Kubernetes as evidenced by the `k8s/` directory.

**Development Environment**: The `.devcontainer/` directory indicates a commitment to reproducible development environments.

## Development Workflow

**Code Reviews**: All pull requests MUST undergo at least one thorough code review by a team member. Reviews MUST verify adherence to these principles, code quality, and test coverage.

**Testing Gates**: Successful execution of all unit and integration tests is a mandatory gate for merging any code.

**Continuous Integration**: Automated builds and tests MUST be executed on every commit to the main development branches.

## Governance
This Constitution supersedes all other informal practices and documentation. Amendments to this Constitution require a formal proposal, documented justification, team approval, and a migration plan if necessary. Compliance with this Constitution is mandatory for all code merged into the main branches.

**Version**: 1.0.0 | **Ratified**: 2026-09-01 | **Last Amended**: 2026-09-01