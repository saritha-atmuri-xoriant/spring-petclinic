# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). No cross-layer dependencies are permitted except for those explicitly defined by the framework (e.g., Controller depending on Service, Service depending on Repository).

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities. Custom configurations MUST be minimal and clearly justified, documented within their respective configuration classes (e.g., `CacheConfiguration`, `WebConfiguration`).

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST verify individual component logic, while integration tests MUST validate interactions between components and with external systems (e.g., database). Existing tests MUST be maintained and extended as needed.

### IV. Data Persistence Abstraction
Data access MUST be exclusively handled through Spring Data JPA repositories. Direct SQL manipulation or manual JDBC operations are forbidden. Repository interfaces MUST define clear contracts for data operations.

### V. RESTful API Design
Controllers MUST expose RESTful endpoints following standard HTTP methods and status codes. Request and response payloads SHOULD be designed for clarity and efficiency, leveraging JSON where appropriate.

## Additional Constraints

The project MUST adhere to the following constraints:
*   **Technology Stack**: Java 17+, Spring Boot 3.x, Spring Data JPA, Thymeleaf for templating.
*   **Database**: Support for multiple database integrations (e.g., H2, PostgreSQL, MySQL) as demonstrated by integration tests.
*   **Internationalization (i18n)**: All user-facing strings MUST be externalized and managed via properties files, as enforced by `I18nPropertiesSyncTest`.

## Development Workflow

*   **Branching Strategy**: Feature branches MUST be created from the `main` branch. All changes MUST be submitted via Pull Requests (PRs).
*   **Code Reviews**: All PRs MUST undergo at least one approval from a team member familiar with the project's architecture and principles. Reviews MUST verify adherence to this constitution.
*   **CI/CD Pipeline**: The CI pipeline MUST include static analysis, unit tests, and integration tests. Successful execution of all tests is a prerequisite for merging.

## Governance

This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a migration plan for existing code to ensure compliance. All Pull Requests and code reviews MUST verify compliance with the principles outlined herein.

**Version**: 1.0.0 | **Ratified**: 2026-08-30 | **Last Amended**: 2026-08-30