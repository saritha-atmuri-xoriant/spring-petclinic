# Feature Specification: Owners for Spring-Petclinic

**Feature Branch**: `008-owners-spring-petclinic`

**Created**: 2026-08-29

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's detail page.

**Why this priority**: This is a core functionality for managing pet owners and is crucial for day-to-day operations.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and submitting. The system should then display the details of the owner named Franklin.

**Acceptance Scenarios**:

1. **Given** an owner named "John Franklin" exists, **When** a user searches for owners with the last name "Franklin", **Then** the system displays the detail page for "John Franklin".

---

### User Story 2 - Find Owners with Partial Last Name Match (Priority: P2)

Given owners with last names starting with "Frank" exist, When a user searches for owners with the last name "Frank", Then a list of owners whose last names start with "Frank" is displayed.

**Why this priority**: This provides flexibility in searching and helps users find owners even if they don't recall the exact spelling.

**Independent Test**: Can be tested by searching for a partial last name like "Frank" and verifying that all owners whose last names begin with "Frank" are listed.

**Acceptance Scenarios**:

1. **Given** owners "John Franklin" and "Jane Frank" exist, **When** a user searches for owners with the last name "Frank", **Then** a list containing both "John Franklin" and "Jane Frank" is displayed.

---

### User Story 3 - Handle Empty Last Name Search (Priority: P3)

Given multiple owners exist, When a user searches for owners with an empty last name, Then all owners are displayed.

**Why this priority**: This is a common user expectation for search functionality, providing a way to view all records.

**Independent Test**: Can be tested by leaving the last name search field empty and submitting the search form. The system should then display a list of all registered owners.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** a user searches for owners with an empty last name, **Then** all owners are displayed in the search results.

---

### Edge Cases

- What happens when an owner's first name is blank? → Validation error.
- What happens when an owner's last name is blank? → Validation error.
- What happens when an owner's address is blank? → Validation error.
- What happens when an owner's city is blank? → Validation error.
- What happens when an owner's telephone number is not 10 digits? → Validation error.
- What happens when a pet's name is blank? → Validation error.
- What happens when a pet's type is not selected? → Validation error.
- What happens when a pet's birth date is in an invalid format? → Validation error.
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error.
- What happens when attempting to add a visit for a pet that does not exist for a given owner? → `IllegalArgumentException` is thrown.
- What happens when attempting to add a visit for an owner that does not exist? → `IllegalArgumentException` is thrown.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details (address, city, telephone).
- **FR-003**: System MUST allow the creation of a new pet for an existing owner.
- **FR-004**: System MUST allow the update of an existing pet's details (name, birth date, type).
- **FR-005**: System MUST allow adding a new visit for a pet.
- **FR-006**: System MUST allow searching for owners by last name.
- **FR-007**: System MUST validate owner information during creation or update.
- **FR-008**: System MUST validate pet information during creation or update.
- **FR-009**: System MUST validate visit information during creation.
- **FR-010**: System MUST display a list of all owners when no last name is provided in the search.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details and associated pets.
    - Attributes: address, city, telephone.
    - Relationships: Has many pets.
- **Pet**: Represents a pet belonging to an owner.
    - Attributes: name, birthDate.
    - Relationships: Belongs to an owner, has a type, has many visits.
- **PetType**: Represents the type of a pet (e.g., cat, dog).
    - Attributes: name.
- **Visit**: Represents a visit to the clinic for a pet.
    - Attributes: date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully search for and view owner details within 5 seconds.
- **SC-002**: Owner creation and update operations complete within 3 seconds.
- **SC-003**: Adding a new pet or visit for an owner completes within 4 seconds.
- **SC-004**: 95% of owner searches return results within the expected time frame.
- **SC-005**: All validation errors for owner, pet, and visit data are clearly presented to the user.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing `Person` entity for owner's first and last name.
- The `spring-petclinic` application is already set up with necessary dependencies for persistence and validation.
- The `OwnerController` will handle the primary user interactions for managing owners and their pets.
- The `PetValidator` will be utilized for validating pet data.
- The `VisitController` will handle adding new visits.