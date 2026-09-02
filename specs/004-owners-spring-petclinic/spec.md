# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `004-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for managing pet owners and is essential for basic system operation.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and verifying redirection to the correct owner's detail page. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** an owner named "John Franklin" exists, **When** the user searches for owners with the last name "Franklin", **Then** the system displays the details page for John Franklin.

---

### User Story 2 - Find Owners with Partial Last Name Match (Priority: P2)

Given multiple owners exist whose last names start with "Frank", When a user searches for owners with the last name "Frank", Then a list of all matching owners is displayed.

**Why this priority**: This enhances the search functionality, allowing users to find owners even if they don't know the exact last name.

**Independent Test**: Can be fully tested by creating multiple owners with last names starting with "Frank" (e.g., "Frank Smith", "Frank Jones"), searching for "Frank", and verifying that all relevant owners are listed. Delivers a more flexible owner search.

**Acceptance Scenarios**:

1. **Given** owners "John Frank" and "Jane Franklin" exist, **When** the user searches for owners with the last name "Frank", **Then** a list containing both "John Frank" and "Jane Franklin" is displayed.

---

### User Story 3 - Handle Empty Search for Last Name (Priority: P3)

Given multiple owners exist, When a user searches for owners with an empty last name or only whitespace, Then all owners are displayed.

**Why this priority**: This ensures a predictable and user-friendly behavior for incomplete searches, preventing unexpected errors.

**Independent Test**: Can be fully tested by having several owners in the system, performing a search with an empty last name field, and verifying that all owners are displayed. Delivers a robust search experience.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** the user searches for owners with an empty last name field, **Then** all existing owners are displayed.

---

### Edge Cases

- What happens when an owner is created or updated with a blank first name? → Validation error.
- What happens when an owner is created or updated with a blank last name? → Validation error.
- How does the system handle an owner's telephone number that does not match the `\d{10}` pattern? → Validation error.
- What happens when an owner is created or updated with a blank address? → Validation error.
- What happens when an owner is created or updated with a blank city? → Validation error.
- How does the system handle an attempt to edit an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- How does the system handle an attempt to create a pet for an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- How does the system handle an attempt to create a visit for an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- How does the system handle an attempt to create a visit for a pet with an ID that does not exist for a given owner? → `IllegalArgumentException` is thrown.
- What happens when a pet is created or updated with a blank name? → Validation error.
- How does the system handle pet creation or update without selecting a pet type? → Validation error.
- What happens when a pet is created or updated with a null birth date? → Validation error.
- How does the system handle an attempt to save a pet with a name that already exists for the same owner? → The scenario is handled, preventing duplicate pet names for the same owner.
- How does the system handle visit creation with a date that is not in the future? → Validation error.
- What happens when a pet update includes an incorrectly formatted birth date (e.g., "2015/02/12")? → Validation error `typeMismatch`.
- How does the system handle searching for owners with a last name that yields no results? → A `notFound` validation error is applied to the `lastName` field.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new pets for an owner.
- **FR-002**: System MUST allow updating an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow searching for owners by last name.
- **FR-005**: System SHOULD display a list of pets associated with an owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Includes address, city, and telephone number. Can have multiple pets.
- **Pet**: Represents a pet belonging to an owner. Has a name, birth date, and type. Can have multiple visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a veterinary visit for a pet, including a date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find an owner by their last name in under 3 seconds.
- **SC-002**: The system displays a list of all owners when the last name search field is empty or contains only whitespace.
- **SC-003**: 95% of pet creation or update operations complete successfully with valid data.
- **SC-004**: Validation errors for owner and pet data are clearly presented to the user upon submission of invalid information.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing authentication mechanisms if any are present.
- Data for owners and pets will be persisted in a relational database.
- The application will be deployed in an environment where standard Spring Boot conventions are followed.