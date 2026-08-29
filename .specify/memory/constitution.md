# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Components MUST NOT cross layer boundaries inappropriately (e.g., a Controller directly accessing a Repository without a Service intermediary).

### II. Spring Boot Conventions
The project MUST leverage Spring Boot's auto-configuration and idiomatic patterns. Configuration MUST be managed via `application.properties` or `@Configuration` classes. Dependency Injection MUST be achieved through Spring's mechanisms (`@Autowired`, constructor injection).

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed with accompanying unit and integration tests. Unit tests MUST focus on individual components, while integration tests MUST verify interactions between components and with external systems (like databases). Existing tests MUST be maintained and expanded as the codebase evolves.

### IV. Data Access Abstraction
Data access MUST be performed exclusively through Spring Data repositories or explicitly defined service methods that encapsulate data access logic. Direct SQL queries within controllers or business logic are prohibited.

### V. RESTful API Design
Controllers MUST expose RESTful endpoints following standard HTTP methods (GET, POST, PUT, DELETE) and status codes. Data transfer between client and server MUST utilize JSON.

## Additional Constraints

### Technology Stack
The project MUST utilize Java as the primary programming language, with Spring Boot as the core framework. JPA and Spring Data are the mandated ORM and data access technologies. Thymeleaf is the default view technology.

### Security
Input validation MUST be implemented at the controller layer to prevent common web vulnerabilities. Sensitive data handling MUST adhere to standard security practices, though this project primarily focuses on core functionality rather than advanced security features.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to architectural principles, coding standards, and test coverage.

### Quality Gates
Automated checks, including static analysis, unit tests, and integration tests, MUST pass successfully before a pull request can be merged. Continuous Integration (CI) pipelines MUST enforce these quality gates.

## Governance
This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this constitution require a formal proposal, documentation of the rationale, and approval by the project's lead architect or designated committee. Any approved amendments MUST include a migration plan for existing code to ensure compliance. All pull requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-29 | **Last Amended**: 2026-08-29