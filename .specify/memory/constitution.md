# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Service, Domain, Configuration, Test). Direct dependencies MUST only flow downwards (e.g., Controller can depend on Service, but Service cannot depend on Controller). This ensures modularity and maintainability.

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be clearly documented and justified, adhering to established Spring Boot patterns.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST focus on individual components, while integration tests (e.g., `MySqlIntegrationTests.java`, `CrashControllerIntegrationTests.java`) MUST verify interactions between components and with external systems (like databases). Test coverage metrics MUST be maintained and reviewed.

### IV. Domain-Driven Design Principles
The core domain entities (`Owner.java`, `Pet.java`, `Vet.java`, `Visit.java`, `Specialty.java`) MUST be the central focus. Business logic SHOULD be encapsulated within these domain objects or associated service layers, promoting a clear separation of concerns.

### V. Observability and Debuggability
Application behavior MUST be observable through structured logging and, where applicable, metrics. The use of standard Spring Boot Actuator endpoints or similar mechanisms is encouraged for monitoring.

## Additional Constraints

### Database Agnosticism (for core logic)
While integration tests may target specific databases (e.g., `MySqlIntegrationTests.java`, `PostgresIntegrationTests.java`), the core application logic SHOULD remain as independent as possible from the underlying database implementation. Spring Data JPA repositories facilitate this.

### Internationalization (i18n)
All user-facing text MUST be internationalized using standard Java resource bundles. The `I18nPropertiesSyncTest.java` MUST pass to ensure all strings are translated across supported locales.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to this constitution, code quality, test coverage, and architectural principles.

### Dependency Management
Dependencies MUST be managed via Maven (or an equivalent build tool). Only approved and actively maintained libraries SHOULD be introduced. Major version upgrades MUST be carefully evaluated for compatibility and potential impact.

### Continuous Integration
The project MUST have a CI pipeline that automatically builds, tests, and analyzes the code on every commit. Build failures MUST be addressed immediately.

## Governance
This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this constitution require a formal proposal, review by the core development team, and a documented migration plan if necessary. Compliance with this constitution is a mandatory requirement for all code merged into the main branch.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31