# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Components MUST NOT directly depend on components in lower layers, except for the Service layer which may depend on Repository and Domain/Model layers.

### II. Spring Boot Convention and Configuration
The project MUST leverage Spring Boot conventions for auto-configuration and dependency injection. All custom configurations MUST be defined in `@Configuration` classes, such as `CacheConfiguration.java` and `WebConfiguration.java`.

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and significant modifications MUST be accompanied by unit and integration tests. The existing test suite, covering controllers, services, and models, MUST be maintained and expanded. Integration tests, like `MySqlIntegrationTests.java` and `PostgresIntegrationTests.java`, MUST validate inter-layer communication and persistence.

### IV. Domain Model Integrity
Domain entities (e.g., `Owner.java`, `Pet.java`, `Vet.java`) MUST encapsulate their state and behavior. They MUST adhere to JPA and Jakarta Bean Validation standards for persistence and data integrity.

### V. Observability and Internationalization
The application MUST support internationalization (i18n) as demonstrated by `WebConfiguration.java` and `I18nPropertiesSyncTest.java`. All user-facing strings MUST be managed through resource bundles.

## Development Workflow

### Code Review and Compliance
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the core principles outlined in this constitution, including architectural layering, testing coverage, and configuration standards.

### Branching Strategy
The project will follow a Gitflow-like branching strategy: `main` for production-ready code, `develop` for integration, and feature branches for new development. All code merged into `develop` and `main` MUST pass all automated tests and code reviews.

### Dependency Management
All project dependencies MUST be managed via Maven (`pom.xml`). New dependencies MUST be carefully evaluated for necessity and potential impact on build times and security.

## Governance

This constitution supersedes all other informal development practices. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the changes. All pull requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-30 | **Last Amended**: 2026-08-30