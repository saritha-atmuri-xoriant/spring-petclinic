# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-04

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for managing pet owners and is essential for basic system operation.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and submitting. The system should then display the details for the owner named Franklin.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists in the system, **When** a user navigates to the owner search page and enters "Franklin" into the "Last Name" field and clicks "Search", **Then** the system displays the details page for the owner named Franklin.

---

### User Story 2 - Find Owners with Partial Last Name Match (Priority: P2)

Given owners with last names starting with "Frank" exist, When a user searches for owners with the last name "Frank", Then a list of owners matching the partial name is displayed.

**Why this priority**: This enhances the usability of the search functionality, allowing users to find owners even if they don't recall the exact spelling.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Frank" in the last name field, and submitting. The system should then display a list of all owners whose last names begin with "Frank".

**Acceptance Scenarios**:

1. **Given** multiple owners exist, including "Frank Smith" and "Franklin Jones", **When** a user navigates to the owner search page and enters "Frank" into the "Last Name" field and clicks "Search", **Then** the system displays a list containing both "Frank Smith" and "Franklin Jones".

---

### User Story 3 - Handle Empty Last Name Search (Priority: P3)

Given multiple owners exist, When a user searches for owners with an empty or whitespace-only last name, Then all owners are displayed in a list.

**Why this priority**: This provides a convenient way to view all registered owners, useful for administrative purposes or when the user wants a general overview.

**Independent Test**: Can be fully tested by navigating to the owner search page, leaving the last name field empty or entering only spaces, and submitting. The system should then display a list of all owners.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** a user navigates to the owner search page and leaves the "Last Name" field empty and clicks "Search", **Then** the system displays a list of all registered owners.

---

### Edge Cases

- What happens when an owner is created or updated with a blank address? **Validation error.**
- What happens when an owner is created or updated with a blank city? **Validation error.**
- How does the system handle an owner's telephone number that does not match the 10-digit pattern? **Validation error.**
- What happens when attempting to access or modify an owner with an ID that does not exist? **`IllegalArgumentException` is thrown.**
- What happens when a pet is created or updated with a blank name? **Validation error.**
- What happens when a pet is created or updated without selecting a pet type? **Validation error.**
- What happens when a pet is created or updated with a null birth date? **Validation error.**
- What happens when attempting to add a pet with a name that already exists for the same owner? **Validation error.**
- What happens when a visit is created with a date that is not after the current date? **Validation error.**
- What happens when attempting to add a visit for a pet that does not exist for the specified owner? **`IllegalArgumentException` is thrown.**
- What happens when searching for owners with a last name that yields no results? **Validation error indicating "not found".**
- What happens when navigating to the "/oups" endpoint? **A `RuntimeException` is thrown, showcasing exception handling.**

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow searching for owners by last name.
- **FR-005**: System SHOULD allow adding a new visit for a pet.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Includes address, city, telephone, and a collection of pets.
- **Pet**: Represents a pet. Includes birth date, type, and a collection of visits. Associated with an Owner.
- **PetType**: Represents the type of a pet (e.g., cat, dog).
- **Visit**: Represents a visit to the vet for a pet. Includes a date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: The system displays a list of all owners when the last name search is empty, within 5 seconds.
- **SC-003**: 95% of pet creation/update operations complete successfully with valid data.
- **SC-004**: Validation errors for invalid owner or pet data are displayed to the user immediately upon submission.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing Person class for owner's first and last names.
- Data retention policies for owner and pet information are handled by the underlying persistence layer and are not a direct concern of this feature's scope.
- The primary database technology is relational, with Spring Data JPA for persistence.
- Standard web application security practices will be followed, including input validation.