# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `050-owners-spring-petclinic`

**Created**: 2026-08-30

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for managing owners and is essential for users to locate specific pet owners.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and verifying redirection to the correct owner's detail page.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists in the system, **When** a user navigates to the owner search page and enters "Franklin" into the "Last Name" search field, **Then** the system redirects the user to the detail page for that specific owner.

---

### User Story 2 - Find Owners with Partial Last Name Match (Priority: P2)

Given multiple owners whose last names start with "Frank" exist, When a user searches for owners with the last name "Frank", Then a list of owners matching the partial last name is displayed.

**Why this priority**: This provides flexibility for users when they don't know the exact last name, improving the search experience.

**Independent Test**: Can be fully tested by searching for a partial last name (e.g., "Frank") and verifying that all owners whose last names start with "Frank" are displayed in a list.

**Acceptance Scenarios**:

1. **Given** multiple owners exist with last names starting with "Frank" (e.g., "Franklin", "Frankenstein"), **When** a user navigates to the owner search page and enters "Frank" into the "Last Name" search field, **Then** a list of all owners whose last names begin with "Frank" is displayed.

---

### User Story 3 - Handle Empty Search for Last Name (Priority: P3)

Given multiple owners exist, When a user performs a search with an empty or whitespace-only last name, Then all owners are displayed in the owner list.

**Why this priority**: This ensures a predictable behavior for empty searches, preventing unexpected errors and providing a comprehensive view of all owners.

**Independent Test**: Can be fully tested by performing a search with an empty last name field and verifying that all existing owners are displayed.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** a user navigates to the owner search page and leaves the "Last Name" search field empty or enters only whitespace, **Then** the system displays a list of all registered owners.

---

### Edge Cases

- What happens when an owner's first name is blank during creation or update? → Validation error is displayed.
- What happens when an owner's last name is blank during creation or update? → Validation error is displayed.
- What happens when an owner's address is blank during creation or update? → Validation error is displayed.
- What happens when an owner's city is blank during creation or update? → Validation error is displayed.
- What happens when an owner's telephone number does not match the `\d{10}` pattern during creation or update? → Validation error is displayed.
- What happens when a user attempts to edit or view an owner with an ID that does not exist? → An `IllegalArgumentException` is thrown.
- What happens when a pet's name is blank during creation or update? → Validation error is displayed.
- What happens when a pet is created or updated without selecting a pet type? → Validation error is displayed.
- What happens when a pet is created or updated with a null birth date? → Validation error is displayed.
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error is displayed.
- What happens when a visit is submitted with a date that is not in the future? → Validation error is displayed.
- What happens when attempting to add a visit for an owner ID that does not exist? → An `IllegalArgumentException` is thrown.
- What happens when attempting to add a visit for a pet ID that does not exist for a given owner? → An `IllegalArgumentException` is thrown.
- What happens when navigating to the `/oups` endpoint? → A `RuntimeException` is thrown, leading to an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details (first name, last name, address, city, telephone).
- **FR-003**: System MUST allow the creation of a new pet for an existing owner.
- **FR-004**: System MUST allow the update of an existing pet's details (name, birth date, type).
- **FR-005**: System MUST allow the addition of a new visit for a pet.
- **FR-006**: System MUST validate owner information during creation or update according to defined business rules.
- **FR-007**: System MUST validate pet information during creation or update according to defined business rules.
- **FR-008**: System MUST validate visit information during creation or update according to defined business rules.
- **FR-009**: System MUST allow searching for owners by last name.
- **FR-010**: System MUST disallow direct setting of address and telephone fields via form submission when creating or updating an owner.
- **FR-011**: System MUST disallow direct setting of the ID field via form submission when creating or updating a pet.
- **FR-012**: System MUST disallow direct setting of the ID field via form submission when creating or updating a visit.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents a pet belonging to an owner. Key attributes include name, birth date, and type. A pet belongs to one owner and can have multiple visits.
- **PetType**: Represents the type of pet (e.g., Cat, Dog). Key attribute is the name of the pet type.
- **Visit**: Represents a visit to the clinic for a pet. Key attributes include date and description. A visit is associated with one pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully create and update owner profiles in under 1 minute.
- **SC-002**: Users can successfully add a new pet to an owner's profile in under 45 seconds.
- **SC-003**: Users can successfully add a new visit for a pet in under 30 seconds.
- **SC-004**: Owner search functionality returns results within 2 seconds for searches with up to 1000 owners.
- **SC-005**: 99% of form submissions for owner, pet, and visit data are validated successfully, with clear error messages for invalid data.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms (if any) are handled separately and are not part of this feature's scope.
- The `spring-petclinic` application is already set up with the necessary database and infrastructure.
- The `Person` and `NamedEntity` base classes provide the expected common fields and functionality.
- The `OwnerRepository`, `PetTypeRepository`, and `PetRepository` interfaces are correctly implemented and available for data persistence.
- The `PetValidator` and `OwnerValidator` (implied) are responsible for enforcing business rules.
- The `VisitController` and `PetController` handle the user interface interactions and form submissions.
- The `/oups` endpoint is intended for demonstrating error handling and is not a user-facing feature.