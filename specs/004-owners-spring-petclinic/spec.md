# Feature Specification: Owner Management

**Feature Branch**: `[###-owner-management]`

**Created**: 2026-08-29

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system should redirect to the owner's detail page.

**Why this priority**: This is a core functionality for accessing owner information and is marked as P1 in the provided user stories.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and verifying redirection to the correct owner's detail page.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists, **When** a user searches for owners with the last name "Franklin", **Then** the system should redirect to the owner's detail page for "Franklin".

---

### User Story 2 - Find Owners with Partial Last Name Match (Priority: P2)

Given multiple owners exist whose last names start with "Frank", When a user searches for owners with the last name "Frank", Then a list of owners matching the partial last name should be displayed.

**Why this priority**: This provides flexibility in searching and is marked as P2.

**Independent Test**: Can be fully tested by searching for a partial last name like "Frank" and verifying that all owners whose last names start with "Frank" are displayed in a list.

**Acceptance Scenarios**:

1. **Given** multiple owners exist whose last names start with "Frank", **When** a user searches for owners with the last name "Frank", **Then** a list of owners matching the partial last name "Frank" should be displayed.

---

### User Story 3 - Handle Empty Last Name Search (Priority: P3)

Given multiple owners exist, When a user searches for owners with an empty or whitespace-only last name, Then all owners should be displayed.

**Why this priority**: This handles a common edge case and is marked as P3.

**Independent Test**: Can be fully tested by performing a search with an empty last name field and verifying that all existing owners are displayed.

**Acceptance Scenarios**:

1. **Given** multiple owners exist, **When** a user searches for owners with an empty last name, **Then** all owners should be displayed.

---

### Edge Cases

- What happens when an owner's first name is blank during creation or update? → Validation error.
- What happens when an owner's address is blank during creation or update? → Validation error.
- What happens when an owner's city is blank during creation or update? → Validation error.
- What happens when an owner's telephone number does not match the `\d{10}` pattern? → Validation error.
- What happens when attempting to edit or view an owner with an ID that does not exist? → `IllegalArgumentException` indicating owner not found.
- What happens when attempting to create a pet with a blank name? → Validation error.
- What happens when attempting to create a pet without selecting a pet type? → Validation error.
- What happens when attempting to create a pet with a null birth date? → Validation error.
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error.
- What happens when attempting to create a visit with a date that is not in the future? → Validation error.
- What happens when attempting to create a visit for a pet belonging to a non-existent owner? → `IllegalArgumentException` indicating owner not found.
- What happens when attempting to create a visit for a non-existent pet belonging to an owner? → `IllegalArgumentException` indicating pet not found.
- What happens when searching for an owner by last name that yields no results? → Error message indicating "not found".

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow finding owners by their last name.
- **FR-005**: System SHOULD allow adding a new visit for a pet.
- **FR-006**: System MUST allow the creation of a new owner.
- **FR-007**: System MUST allow the update of an existing owner's details (address, city, telephone).
- **FR-008**: System MUST validate owner information during creation or update, ensuring first name, last name, address, and city are not blank, and telephone is exactly 10 digits.
- **FR-009**: System MUST disallow direct setting of address and telephone fields via form submission when creating or updating an owner.
- **FR-010**: System MUST disallow direct setting of the ID field via form submission when creating or updating a visit.
- **FR-011**: System MUST ensure a pet's name is unique for a given owner.
- **FR-012**: System MUST allow finding owners by partial last name matches.
- **FR-013**: System MUST display all owners when a search for owners with an empty or whitespace-only last name is performed.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual who owns pets. Key attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents an animal owned by an owner. Key attributes include name, birth date, and type. A pet belongs to one owner and can have multiple visits.
- **PetType**: Represents the species of a pet (e.g., Cat, Dog).
- **Visit**: Represents a veterinary visit for a pet. Key attributes include date and description. A visit is associated with a specific pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully find owners by last name in under 3 seconds.
- **SC-002**: The system supports up to 500 concurrent owner searches without performance degradation.
- **SC-003**: 95% of owner creation/update operations complete successfully with valid data.
- **SC-004**: User error rate for owner data entry (e.g., invalid phone number, blank fields) is reduced by 30% due to improved validation.
- **SC-005**: All P1 user stories are implemented and pass their acceptance scenarios.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- Existing authentication mechanisms will be reused if applicable for owner management.
- The `spring-petclinic` application's existing data model and persistence layer will be utilized.
- The `OwnerController` and `PetController` will handle the primary user interactions for managing owners and pets.
- The `Validator` interface and Spring's validation framework will be used for data validation.
- The `LocalDate` type will be used for date fields.
- The `Person` and `NamedEntity` base classes will be extended for owner and pet entities respectively.