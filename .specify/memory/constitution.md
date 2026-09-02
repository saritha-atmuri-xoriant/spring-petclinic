# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Cross-layer dependencies MUST follow a strict unidirectional flow: Controllers depend on Services, Services depend on Repositories, Repositories interact with the data store, and Domain/Model objects are independent. Configuration classes MUST be isolated and only affect application setup.

### II. Spring Boot Convention and Idioms
The project MUST leverage Spring Boot's auto-configuration, starter dependencies, and idiomatic patterns. Configuration MUST be managed via `application.properties` or `application.yml`, and Spring Beans MUST be declared using annotations (`@Component`, `@Service`, `@Repository`, `@Controller`, `@Configuration`) or Java configuration classes.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST focus on individual components in isolation, while integration tests MUST verify the interaction between components and with external systems (e.g., database). Test coverage MUST be tracked and maintained, with a minimum threshold of 80% for critical components.

### IV. Data Persistence Abstraction
Data access MUST be abstracted through Spring Data JPA repositories. Direct SQL queries SHOULD be avoided in favor of repository methods and derived queries. Entity classes MUST be annotated with JPA annotations and adhere to standard ORM practices.

### V. Observability and Logging
All significant application events, errors, and state changes MUST be logged using a structured logging framework (e.g., SLF4j with Logback). Logs MUST be informative and aid in debugging and monitoring. Application health and performance metrics SHOULD be exposed where applicable.

## Development Workflow and Quality Gates

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to architectural principles, coding standards, test coverage, and overall code quality.

### Automated Testing
CI/CD pipelines MUST include automated execution of all unit and integration tests. Builds failing due to test failures MUST be blocked from merging.

### Database Integration Testing
Specific integration tests (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`) MUST be executed to ensure correct database interaction. These tests MAY utilize Testcontainers for isolated database environments.

## Governance
This constitution supersedes all other development practices for the saritha-atmuri-xoriant/spring-petclinic repository. Amendments to this constitution require a formal proposal, review by the core development team, and a documented migration plan if necessary. Compliance with this constitution is mandatory for all code merged into the main branch. Any deviation MUST be explicitly justified and approved.

**Version**: 1.0.0 | **Ratified**: 2026-09-02 | **Last Amended**: 2026-09-02