# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Components MUST NOT directly depend on components in lower layers (e.g., Controllers MUST NOT depend on Repositories).

### II. Spring Boot Convention Over Configuration
The project MUST leverage Spring Boot's auto-configuration capabilities. Custom configurations MUST be minimal and clearly justified, primarily residing in `src/main/java/org/springframework/samples/petclinic/system` or specific module configurations.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and/or integration tests. Unit tests MUST focus on individual components, while integration tests MUST verify interactions between layers and external systems (e.g., database). The `src/test` directory MUST reflect this commitment with well-organized test suites.

### IV. Data Persistence Abstraction
The project MUST utilize Spring Data JPA for data access. Repository interfaces MUST be defined in the `repository` layer, abstracting direct database interactions. Domain entities MUST be annotated with JPA annotations.

### V. RESTful API Design
Controller classes MUST expose RESTful endpoints following standard HTTP methods (GET, POST, PUT, DELETE) and resource-based URLs. Responses SHOULD be structured and consistent, leveraging Spring MVC annotations.

## Additional Constraints

### Technology Stack
The project MUST be built using Java and Spring Boot. Dependencies are managed via Maven. The primary database is assumed to be relational (e.g., MySQL, PostgreSQL, H2), with integration tests for multiple databases present.

### Internationalization (i18n)
All user-facing strings MUST be internationalized and managed through properties files in `src/main/resources`. The `I18nPropertiesSyncTest` MUST pass to ensure consistency across languages.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to these principles, code quality, and test coverage.

### Branching Strategy
A Gitflow-like branching strategy is recommended, with `main` for production-ready code, `develop` for integration, and feature branches for new development.

### Dependency Management
All dependencies MUST be declared in the `pom.xml` file. New dependencies MUST be carefully evaluated for necessity and licensing.

## Governance
This Constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this Constitution require a formal proposal, documented justification, and approval by a majority of the core development team. All existing code MUST be migrated to comply with amended principles within a reasonable timeframe, as defined by the amendment proposal. Compliance with this Constitution is a mandatory quality gate for all code merged into the `main` branch.

**Version**: 1.0.0 | **Ratified**: 2026-09-03 | **Last Amended**: 2026-09-03