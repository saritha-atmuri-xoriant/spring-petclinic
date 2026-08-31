# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Test). Components MUST NOT cross layer boundaries in an unintended manner. This ensures maintainability and separation of concerns.

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations MUST be clearly documented and justified. Avoid unnecessary boilerplate code.

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed with a test-first approach. Unit tests MUST cover individual components, while integration tests MUST validate interactions between layers and external dependencies (e.g., database). Test coverage MUST be maintained at a high level.

### IV. Data Persistence Abstraction
The Repository layer MUST abstract all data access logic. All interactions with the underlying data store (e.g., database) MUST be performed through repository interfaces. Domain entities MUST be POJOs and adhere to JPA standards.

### V. RESTful API Design
Controllers MUST expose RESTful endpoints following standard HTTP methods and status codes. Data transfer between the client and server SHOULD utilize JSON.

## Additional Constraints

### Technology Stack
The project MUST utilize Java, Spring Boot, Spring Data JPA, and Thymeleaf for templating. Database interactions are expected to be with a relational database (e.g., H2, MySQL, PostgreSQL).

### Internationalization (i18n)
All user-facing strings MUST be internationalized using Spring's message source mechanism. The `I18nPropertiesSyncTest` MUST pass, ensuring all strings are translated across all supported locales.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to this constitution, code quality, and test coverage.

### Dependency Management
Dependencies MUST be managed via Maven. New dependencies MUST be added with careful consideration of their impact on the project and security.

### Build and CI/CD
The project MUST have a fully automated build process. Continuous Integration (CI) MUST be configured to run all tests on every commit. Continuous Deployment (CD) pipelines MAY be established for automated deployments to staging and production environments.

## Governance
This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of core maintainers. All pull requests and code reviews must verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31