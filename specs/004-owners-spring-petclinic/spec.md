# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `004-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for managing and accessing owner information, essential for day-to-day operations.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and verifying redirection to the correct owner's detail page. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** an owner named "George Franklin" exists in the system, **When** a user searches for owners with the last name "Franklin", **Then** the system displays the details for George Franklin.
2. **Given** multiple owners exist, including "George Franklin" and "Betty Davis", **When** a user searches for owners with the last name "Franklin", **Then** the system displays the details for George Franklin and not Betty Davis.

---

### User Story 2 - Find Owners with Partial Last Name Match (Priority: P2)

Given multiple owners whose last names start with "Frank" exist, When a user searches for owners with the last name "Frank", Then a list of owners whose last names start with "Frank" is displayed.

**Why this priority**: This provides flexibility in searching when the exact last name is not known, improving user experience.

**Independent Test**: Can be fully tested by searching for a partial last name (e.g., "Frank") and verifying that all owners whose last names begin with "Frank" are displayed in a list. Delivers the ability to find owners with partial name matches.

**Acceptance Scenarios**:

1. **Given** owners "George Franklin", "Frank Smith", and "Jane Doe" exist, **When** a user searches for owners with the last name "Frank", **Then** the system displays a list containing "George Franklin" and "Frank Smith".
2. **Given** no owners have a last name starting with "Fran", **When** a user searches for owners with the last name "Fran", **Then** the system displays a message indicating no owners were found.

---

### User Story 3 - Handle Empty Last Name Search (Priority: P3)

Given multiple owners exist, When a user searches for owners with an empty last name, Then all owners are displayed on the owners list page.

**Why this priority**: This ensures that users can retrieve a complete list of all owners when no specific search criteria are provided.

**Independent Test**: Can be fully tested by navigating to the owner search page, leaving the last name field empty, and verifying that all existing owners are displayed. Delivers the ability to view all owners.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** a user searches for owners with an empty last name, **Then** the system displays a list of all registered owners.
2. **Given** no owners exist in the system, **When** a user searches for owners with an empty last name, **Then** the system displays a message indicating no owners were found.

---

### Edge Cases

- What happens when an owner is created or updated with a blank address? → A validation error is displayed, and the operation fails.
- What happens when an owner is created or updated with a blank city? → A validation error is displayed, and the operation fails.
- What happens when an owner's telephone number does not match the 10-digit pattern? → A validation error is displayed, and the operation fails.
- What happens when a pet is created or updated with a blank name? → A validation error is displayed, and the operation fails.
- What happens when a pet is created or updated without selecting a pet type? → A validation error is displayed, and the operation fails.
- What happens when a pet is created or updated without providing a birth date? → A validation error is displayed, and the operation fails.
- What happens when attempting to add a pet with a name that already exists for the same owner? → A validation error is displayed, and the operation fails.
- What happens when attempting to create a visit with a date that is not after the current date? → A validation error is displayed, and the operation fails.
- What happens when attempting to find an owner with an ID that does not exist? → An `IllegalArgumentException` is thrown, and an appropriate error message is displayed to the user.
- What happens when attempting to create a visit for a pet belonging to a non-existent owner? → An `IllegalArgumentException` is thrown, and an appropriate error message is displayed to the user.
- What happens when attempting to create a visit for a non-existent pet belonging to an owner? → An `IllegalArgumentException` is thrown, and an appropriate error message is displayed to the user.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details (address, city, telephone).
- **FR-003**: System MUST allow the creation of a new pet for a given owner.
- **FR-004**: System MUST allow the update of an existing pet's name and birth date.
- **FR-005**: System MUST allow the creation of a new visit for a given pet.
- **FR-006**: System MUST validate owner information during creation or update (address, city, telephone).
- **FR-007**: System MUST validate pet information during creation or update (name, type, birth date).
- **FR-008**: System MUST validate visit information during creation (date, description).
- **FR-009**: System MUST allow searching for owners by last name.
- **FR-010**: System MUST allow retrieving a specific owner by their ID.
- **FR-011**: System MUST prevent a pet's name from being duplicated within the same owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual owner of pets. Attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents an animal owned by an owner. Attributes include name, birth date, and type. A pet belongs to one owner and can have multiple visits.
- **PetType**: Represents the species of a pet (e.g., Cat, Dog).
- **Visit**: Represents a veterinary visit for a pet. Attributes include date and description. A visit is associated with one pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully create and update owner profiles in under 1 minute.
- **SC-002**: Users can successfully add a new pet to an owner's profile in under 45 seconds.
- **SC-003**: Search for owners by last name returns results in under 2 seconds.
- **SC-004**: 95% of owner and pet data entries are valid according to defined business rules.
- **SC-005**: The system successfully handles all defined edge cases without crashing or data corruption.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing authentication mechanisms if applicable (though not explicitly detailed in the provided context).
- Data validation rules (e.g., telephone format, date formats) are strictly enforced as per the provided business rules.
- The "owners" module is a core part of the Spring Petclinic application and will be integrated as such.
- The `SPECIFY_FEATURE_DIRECTORY` will be `specs/001-owners-management` based on sequential numbering.
- The `spec-template` used is the default one provided.
- No specific Git branch name was provided by the user, so no `before_specify` hook for branch creation is expected to be triggered with a specific name.
- No `after_specify` hooks are defined in `.specify/extensions.yml` based on the provided context.