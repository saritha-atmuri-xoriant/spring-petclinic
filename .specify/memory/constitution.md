# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Components MUST NOT cross layer boundaries in an unintended direction (e.g., a Controller directly calling a Repository without service intervention).

### II. Spring Boot Convention and Best Practices
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Dependencies and configurations MUST align with Spring Boot's established conventions for web applications, data access, and testing.

### III. Test-Driven Development and Comprehensive Testing
All new features and bug fixes MUST be developed with a test-first approach. Unit tests MUST cover individual components, integration tests MUST validate interactions between layers and external systems (e.g., databases), and end-to-end tests (where applicable) MUST verify user flows. Tests MUST be executable via standard build tools (e.g., Maven, Gradle).

### IV. Data Persistence Abstraction
Data access MUST be managed through Spring Data repositories. Direct SQL queries or manual JDBC operations are DISCOURAGED and should only be used in exceptional circumstances with strong justification. Entities MUST be mapped using JPA annotations.

### V. Observability and Internationalization
The application MUST support internationalization (i18n) for user-facing messages, as evidenced by the presence of i18n properties files and related configuration. Logging MUST be implemented to facilitate debugging and monitoring.

## Additional Constraints

The project MUST utilize Java as the primary programming language.
The project MUST be built using Maven.
The project MUST be containerized using Docker, with Kubernetes deployment manifests provided in the `k8s/` directory.
The project MUST adhere to the Java Bean Validation API for data integrity.

## Development Workflow

All code changes MUST be submitted as Pull Requests (PRs).
Each PR MUST include sufficient unit and integration tests to cover the changes.
All PRs MUST undergo a code review by at least one other team member.
Successful completion of all automated tests and a successful code review are mandatory quality gates for merging.
New features or significant refactorings may require architectural review.

## Governance
This constitution supersedes all other development practices for the saritha-atmuri-xoriant/spring-petclinic repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team. Any approved amendments must include a plan for migrating existing code and practices to comply with the new rules. All Pull Requests and code reviews must verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-01 | **Last Amended**: 2026-09-01