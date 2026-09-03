# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Cross-layer dependencies MUST follow a strict top-down flow (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between unrelated layers are forbidden.

### II. Spring Boot Convention and Idioms
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Configuration MUST be managed via `@Configuration` classes and properties files. Dependency Injection MUST be used extensively via `@Autowired` and constructor injection.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST focus on individual components, while integration tests MUST verify interactions between components and with external systems (e.g., database). Test coverage MUST be maintained above 80%.

### IV. Data Persistence Abstraction
Data access MUST be abstracted through Spring Data JPA repositories. All entities MUST be mapped to database tables using JPA annotations. Direct SQL queries SHOULD be avoided in favor of repository methods and Spring Data JPA query derivation.

### V. RESTful API Design
Controllers MUST expose RESTful endpoints following standard HTTP methods (GET, POST, PUT, DELETE) and status codes. Request and response payloads SHOULD be in JSON format.

## Additional Constraints

### Security Requirements
All sensitive data handling MUST adhere to Spring Security best practices. Input validation MUST be implemented at the controller layer to prevent common web vulnerabilities.

### Performance Standards
Database queries MUST be optimized for performance. Caching mechanisms (e.g., JCache) SHOULD be utilized for frequently accessed, read-heavy data. Performance regressions MUST be identified and addressed during integration testing.

## Development Workflow

### Code Review Process
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to architectural principles, coding standards, and test coverage requirements.

### Quality Gates
Automated checks, including static code analysis, unit tests, and integration tests, MUST pass before code can be merged into the main branch. Any failure in these gates will block the merge.

## Governance
This constitution supersedes all other informal practices and documentation. Amendments to this constitution require a formal proposal, review by the architecture team, and a majority approval from project stakeholders. All amendments MUST include a clear migration plan if necessary. Compliance with this constitution is mandatory for all code merged into the repository.

**Version**: 1.0.0 | **Ratified**: 2026-09-03 | **Last Amended**: 2026-09-03