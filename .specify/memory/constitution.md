# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain, Configuration, Test). Direct dependencies MUST only flow downwards (e.g., Controller can depend on Service, but Service cannot depend on Controller). This ensures maintainability and clear separation of concerns.

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration`, `WebConfiguration`) MUST be minimal, well-documented, and justified by specific project needs beyond standard Spring Boot defaults.

### III. Test-Driven Development (TDD) and Comprehensive Testing
All new features and bug fixes MUST be developed following a TDD approach. Unit tests MUST cover individual components, integration tests MUST validate interactions between components and external systems (like databases), and end-to-end tests (where applicable) MUST verify user flows. The presence of extensive test files (e.g., `OwnerControllerTests.java`, `ClinicServiceTests.java`, `MySqlIntegrationTests.java`) indicates a strong existing testing culture that MUST be maintained and expanded.

### IV. Domain-Driven Design Principles
The core domain entities (`Owner`, `Pet`, `Vet`, `Visit`, `PetType`, `Specialty`) MUST be clearly defined and adhere to the `BaseEntity` and `NamedEntity` patterns. Business logic SHOULD be encapsulated within these domain objects or associated service layers, rather than being scattered across controllers or utility classes.

### V. Observability and Configuration Management
Application behavior MUST be configurable through standard Spring Boot mechanisms (e.g., `application.properties`, environment variables). Logging MUST be structured and informative, aiding in debugging and monitoring. The presence of `CacheConfiguration` suggests that caching strategies are important and should be managed and monitored.

## Additional Constraints

The project MUST utilize Java as the primary programming language and Spring Boot as the core framework. JPA and Hibernate are the established persistence technologies. Testing frameworks like JUnit 5 and AssertJ MUST be used for all test suites. Kubernetes deployment configurations are present in the `k8s/` directory, indicating a deployment target that should be considered during development.

## Development Workflow

All code changes MUST be submitted via Pull Requests (PRs). Each PR MUST include comprehensive unit and integration tests. Code reviews MUST be performed by at least one other team member, focusing on adherence to these principles, code quality, and test coverage. Automated checks (CI pipelines) MUST verify build success, test execution, and static analysis results before merging.

## Governance

This Constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this Constitution require a formal proposal, review by core team members, and a majority approval. Any approved amendments MUST include a clear migration plan for existing code and documentation. All Pull Requests and code reviews MUST verify compliance with this Constitution.

**Version**: 1.0.0 | **Ratified**: 2026-09-04 | **Last Amended**: 2026-09-04