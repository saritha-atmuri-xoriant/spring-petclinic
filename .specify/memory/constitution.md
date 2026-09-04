# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain, Configuration, Test). Direct dependencies MUST only flow downwards (e.g., Controller can depend on Service, Service on Repository, but not vice-versa).

### II. Spring Boot Conventions
The project MUST leverage Spring Boot features and conventions for configuration, dependency injection, and application bootstrapping. This includes utilizing `@SpringBootApplication`, auto-configuration, and standard Spring annotations.

### III. Test-Driven Development (TDD) & Comprehensive Testing
All new features and bug fixes MUST be developed with a test-first approach. Unit tests MUST cover individual components, while integration tests MUST validate interactions between layers and external systems (e.g., database, external APIs). All tests MUST pass before code is merged.

### IV. Data Persistence Abstraction
Data access MUST be abstracted through Spring Data repositories. Direct SQL manipulation within business logic is forbidden. All repository interfaces MUST be clearly defined and adhere to Spring Data JPA standards.

### V. Internationalization (i18n) First
All user-facing strings MUST be externalized and managed through i18n properties files. The `I18nPropertiesSyncTest` MUST pass, ensuring all strings are translated across all supported locales.

## Additional Constraints

### Technology Stack
The project MUST be built using Java and Spring Boot. Dependencies MUST be managed via Maven. The primary database technology is assumed to be relational (e.g., H2, PostgreSQL, MySQL), with Spring Data JPA for persistence.

### Security
While not explicitly detailed in the provided files, standard web application security practices SHOULD be followed, including input validation and protection against common vulnerabilities.

### Observability
The application SHOULD be instrumented for monitoring and logging. Spring Boot Actuator and standard logging frameworks (e.g., SLF4j with Logback) are expected to be used.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to these principles, coding standards, and overall code quality.

### Quality Gates
Automated checks, including compilation, static analysis (e.g., SonarQube), and all unit and integration tests, MUST pass successfully before a pull request can be merged.

### Database Migrations
Any schema changes MUST be managed through a database migration tool (e.g., Flyway, Liquibase), with migration scripts committed to the repository.

## Governance

This Constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this Constitution require a formal proposal, documented justification, and approval by a majority of core maintainers. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the changes. All pull requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-04 | **Last Amended**: 2026-09-04