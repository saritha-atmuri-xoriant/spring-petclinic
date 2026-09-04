# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Cross-layer dependencies MUST follow a strict top-down flow (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between unrelated layers (e.g., Controllers directly accessing Repositories) are forbidden.

### II. Spring Boot Conventions
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Configuration files (e.g., `application.properties`, `application.yml`) MUST be used for application-wide settings. Spring Beans MUST be declared using standard annotations (`@Component`, `@Service`, `@Repository`, `@Controller`, `@Configuration`).

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST focus on individual components, while integration tests MUST verify interactions between components and with external systems (e.g., database). Test coverage MUST be maintained above 80% for critical components.

### IV. Domain-Driven Design Principles
Domain entities (e.g., `Owner`, `Pet`, `Vet`) MUST encapsulate their data and behavior. Business logic MUST reside within the domain or service layers, not within controllers or repositories. Value objects and aggregates MUST be used where appropriate to model the domain accurately.

### V. Observability and Logging
All components MUST implement structured logging using a standard logging framework (e.g., SLF4j with Logback). Critical events, errors, and performance metrics MUST be logged to facilitate debugging and monitoring. The `CacheConfiguration` indicates an awareness of performance optimization, which should be further supported by logging cache hits/misses where relevant.

## Development Workflow and Quality Gates

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to the project's core principles, coding standards, and test coverage requirements.

### Testing Gates
Automated tests MUST pass in the CI pipeline before any code can be merged. Integration tests, particularly those involving database interactions (e.g., `MySqlIntegrationTests`, `PostgresIntegrationTests`), MUST be executed as part of the CI process.

### Dependency Management
Dependencies MUST be managed using Maven (as indicated by `pom.xml` structure). Only well-maintained and necessary dependencies are permitted. Updates to dependencies MUST be accompanied by regression testing.

## Governance
This constitution supersedes all other informal practices and guidelines within this repository. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a plan for migrating existing code and practices to comply with the new rules. All pull requests and code reviews MUST explicitly verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-04 | **Last Amended**: 2026-09-04