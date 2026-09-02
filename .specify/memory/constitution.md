# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Service, Model, Configuration, Test). Components MUST NOT cross layer boundaries in an unintended manner (e.g., a Controller directly calling a Repository without service intervention).

### II. Spring Boot Convention and Idiomatic Usage
The project MUST leverage Spring Boot features and conventions. This includes, but is not limited to, the use of `@SpringBootApplication`, auto-configuration, dependency injection via `@Autowired`, and standard Spring MVC patterns for web controllers.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and/or integration tests. Unit tests MUST focus on individual components, while integration tests MUST verify interactions between components and with external systems (e.g., database). Existing tests MUST be maintained and updated as code evolves.

### IV. Data Access Abstraction
Data access logic MUST be encapsulated within Repository interfaces, leveraging Spring Data JPA. Direct SQL queries or manual data manipulation outside of repository methods are discouraged unless absolutely necessary and well-justified.

### V. Observability and Configuration
Application configuration MUST be managed through standard Spring Boot mechanisms (e.g., `application.properties`, environment variables). Logging MUST be implemented using SLF4j/Logback, with appropriate levels for different environments. Cache configurations, as seen in `CacheConfiguration.java`, MUST be clearly defined and utilized.

## Additional Constraints

### Database Agnosticism (via Test Configurations)
While integration tests exist for specific databases (e.g., `MySqlIntegrationTests.java`, `PostgresIntegrationTests.java`), the core application logic SHOULD remain as database-agnostic as possible, relying on JPA abstractions.

### Internationalization (i18n) Support
All user-facing strings MUST be internationalized and managed via properties files, as enforced by `I18nPropertiesSyncTest.java`.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to architectural principles, coding standards, and test coverage.

### Branching Strategy
A Gitflow-like branching strategy is recommended, with `main` for production-ready code, `develop` for integration, and feature branches for new development.

### Dependency Management
Dependencies MUST be managed via Maven (`pom.xml`). Any new dependencies MUST be carefully evaluated for necessity and licensing.

## Governance
This constitution supersedes all other informal development practices. Amendments to this constitution require a formal proposal, review by the core development team, and a documented migration plan if necessary. Compliance with this constitution is a mandatory part of the code review process. Any deviation from these principles MUST be explicitly justified and approved.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02