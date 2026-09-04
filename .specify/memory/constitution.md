# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Enforcement
Every component MUST reside within its designated architectural layer (Controller, Repository, Service, Domain, Configuration, Test). Cross-layer dependencies MUST adhere to a strict unidirectional flow: Controllers depend on Services, Services depend on Repositories and Domain models, Repositories interact with data sources, and Domain models are self-contained. Configuration classes MUST be isolated and only affect application setup. Test classes MUST NOT introduce dependencies into production code.

### II. Spring Boot Convention Adherence
The project MUST leverage Spring Boot conventions for configuration, auto-configuration, and dependency injection. Application startup MUST be handled by `PetClinicApplication.java`. Configuration properties MUST be managed via standard Spring Boot mechanisms.

### III. Test Coverage Mandate (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by comprehensive unit and integration tests. Unit tests MUST focus on individual components, while integration tests MUST verify interactions between components and with external systems (e.g., databases). Existing test suites (e.g., `OwnerControllerTests.java`, `ClinicServiceTests.java`) MUST be maintained and expanded.

### IV. Data Persistence Abstraction
Data access MUST be abstracted through Spring Data JPA repositories. All database interactions MUST be encapsulated within repository interfaces (`OwnerRepository.java`, `VetRepository.java`, etc.). Direct SQL queries or manual JDBC operations within service or controller layers are forbidden.

### V. RESTful API Design
Controller classes (`OwnerController.java`, `PetController.java`, etc.) MUST implement RESTful APIs following standard HTTP methods and status codes. Request and response payloads SHOULD be structured using appropriate data transfer objects (DTOs) or domain entities.

## Additional Constraints

The project MUST utilize Java as the primary programming language.
The project MUST be built using Maven.
The project MUST be compatible with recent stable versions of Spring Boot.
The project MUST support internationalization (i18n) as evidenced by `I18nPropertiesSyncTest.java` and `WebConfiguration.java`.

## Development Workflow

Code changes MUST be submitted via Pull Requests.
All Pull Requests MUST undergo a thorough code review by at least one other team member.
Code reviews MUST verify adherence to the Core Principles and architectural guidelines.
Automated tests MUST pass on every commit and before merging any Pull Request.
The `k8s/` directory indicates potential for containerized deployments, and any changes affecting deployment MUST consider this.

## Governance

This Constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository.
Amendments to this Constitution require a formal proposal, documentation of the rationale, and approval by a majority of the core development team.
All Pull Requests and code reviews MUST explicitly verify compliance with this Constitution.
Any deviation from these principles MUST be clearly justified and documented in the Pull Request.

**Version**: 1.0.0 | **Ratified**: 2026-09-04 | **Last Amended**: 2026-09-04