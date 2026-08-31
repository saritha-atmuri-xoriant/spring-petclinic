# Spring Petclinic Constitution

## Core Principles

### I. Layered Architecture Adherence
Every component MUST reside within its designated architectural layer (Controller, Repository, Domain/Model, Configuration, Service, Test). Cross-layer dependencies MUST follow a strict top-down flow (e.g., Controllers depend on Services, Services depend on Repositories). Direct dependencies between non-adjacent layers are prohibited.

### II. Spring Boot Convention Over Configuration
Leverage Spring Boot's auto-configuration capabilities wherever possible. Custom configurations (e.g., `CacheConfiguration.java`, `WebConfiguration.java`) MUST be minimal, well-documented, and justified by specific project needs beyond standard Spring Boot defaults.

### III. Comprehensive Test Coverage (NON-NEGOTIABLE)
All new features and bug fixes MUST be accompanied by unit and integration tests. Unit tests MUST cover individual components (controllers, services, models), while integration tests MUST verify interactions between components and with external systems (e.g., database, external APIs). Test coverage MUST be tracked and maintained, with a minimum threshold of 80% for critical components.

### IV. JPA Repository Best Practices
JPA repositories (e.g., `OwnerRepository.java`, `VetRepository.java`) MUST be used for data access. Custom query methods SHOULD be defined within the repository interfaces. Avoid complex business logic within repositories; delegate such logic to the service layer.

### V. RESTful API Design
Controllers (e.g., `OwnerController.java`, `PetController.java`) MUST adhere to RESTful principles for API design. Use standard HTTP methods (GET, POST, PUT, DELETE) appropriately. Responses SHOULD be in JSON format, and error handling MUST be consistent and informative.

## Additional Constraints

### Database Agnosticism
While integration tests may target specific databases (e.g., `MySqlIntegrationTests.java`, `PostgresIntegrationTests.java`), the core application logic MUST remain agnostic to the underlying database technology. Use JPA and Spring Data JPA to abstract database interactions.

### Internationalization (i18n)
All user-facing strings MUST be internationalized using Spring's message source mechanism. The `I18nPropertiesSyncTest.java` serves as a gate to ensure all strings are properly translated across supported locales.

## Development Workflow

### Code Reviews
All pull requests MUST undergo a thorough code review by at least one other team member. Reviews MUST verify adherence to this constitution, code quality, test coverage, and overall design.

### Dependency Management
External dependencies MUST be managed via Maven. New dependencies MUST be carefully evaluated for necessity and potential impact on the project.

Governance
This constitution supersedes all other development practices for the `saritha-atmuri-xoriant/spring-petclinic` repository. Amendments to this constitution require a formal proposal, documented justification, and approval by a majority of the core development team. Any approved amendments MUST include a migration plan to ensure existing code adheres to the new principles. All pull requests and code reviews MUST verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: 2026-08-31 | **Last Amended**: 2026-08-31