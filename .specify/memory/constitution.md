# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain, Configuration, Test). Direct dependencies MUST only flow downwards (e.g., Controller can depend on Service, Service on Repository, but not vice-versa). This ensures maintainability and separation of concerns.

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be minimal and clearly justified, adhering to established Spring patterns.

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed following a TDD approach. Unit tests MUST cover individual components, while integration tests (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`) MUST validate interactions between components and with external systems like databases. Test coverage MUST be maintained at a high level, with specific focus on controller endpoints, repository interactions, and core domain logic.

### IV. Explicit Dependency Management
Dependencies between modules and classes MUST be explicitly declared and managed, primarily through Spring's dependency injection mechanisms. Avoid implicit dependencies or tightly coupled components that are not managed by the Spring container.

### V. Internationalization (i18n) First
All user-facing strings MUST be externalized and managed through i18n properties files. The `I18nPropertiesSyncTest` MUST pass, ensuring all strings are translated across all supported locales.

## Additional Constraints

### Database Agnosticism
While integration tests may target specific databases (MySQL, PostgreSQL), the core application logic MUST remain agnostic to the underlying database technology. Data access layers (Repositories) SHOULD abstract database-specific details.

### Security Best Practices
All web endpoints MUST be secured according to standard Spring Security practices. Input validation MUST be implemented at the controller layer and within domain models to prevent common vulnerabilities.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to this constitution, architectural principles, coding standards, and test coverage.

### Branching Strategy
A Gitflow-like branching strategy is recommended, with `main` for production-ready code, `develop` for integration, and feature branches for new development.

### CI/CD Integration
The repository MUST integrate with a Continuous Integration/Continuous Deployment pipeline. All commits to `develop` and `main` branches MUST trigger automated builds, tests, and deployments.

## Governance

This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this constitution require a formal proposal, review by the core development team, and a majority approval. Any approved amendments MUST include a migration plan to ensure existing code adheres to the new principles. Compliance with this constitution is a mandatory requirement for all code merged into the repository.

**Version**: 1.0.0 | **Ratified**: 2026-08-29 | **Last Amended**: 2026-08-29