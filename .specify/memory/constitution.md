# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain, Configuration, Test). Cross-layer dependencies MUST strictly follow the defined hierarchy (e.g., Controllers depend on Services, Services depend on Repositories).

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be minimal, well-documented, and only introduced when explicit deviation from convention is necessary and justified.

### III. Test-Driven Development and Comprehensive Testing
All new features and bug fixes MUST be developed with a test-first approach. Unit tests MUST cover individual components, integration tests MUST validate inter-layer and inter-service communication, and end-to-end tests (where applicable) MUST ensure overall application functionality. The existing test suite structure (e.g., `OwnerControllerTests`, `ClinicServiceTests`) MUST be maintained and expanded.

### IV. JPA Repository Best Practices
JPA repositories (e.g., `OwnerRepository`, `VetRepository`) MUST be used for data access. Custom query methods SHOULD be defined within these repositories, and direct SQL manipulation SHOULD be avoided in favor of the ORM's capabilities.

### V. Internationalization (i18n) Compliance
All user-facing strings MUST be externalized and managed through i18n properties files. The `I18nPropertiesSyncTest` MUST pass, ensuring all strings are translated across all supported locales.

## Additional Constraints

The project MUST utilize Java as the primary programming language and Spring Boot as the core framework. Dependencies MUST be managed via Maven. Database interactions MUST be handled through JPA and Spring Data JPA.

## Development Workflow

All code changes MUST be submitted as Pull Requests (PRs). Each PR MUST include sufficient unit and integration tests to cover the changes. Code reviews MUST be performed by at least one other team member, with a focus on adherence to these principles, code quality, and test coverage. CI/CD pipelines MUST enforce these checks before merging.

## Governance

This Constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this Constitution require a formal proposal, review by the core development team, and a documented migration plan if necessary. All Pull Requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-04 | **Last Amended**: 2026-09-04