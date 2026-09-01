# Feature Specification: owners for spring-petclinic

**Feature Branch**: `027-owners-spring-petclinic`

**Created**: 2026-09-01

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing clinic operations and is essential for day-to-day use.

**Independent Test**: Can be fully tested by entering a known owner's last name and verifying their details are displayed.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists, **When** a user searches for owners with the last name "Franklin", **Then** the system redirects to the owner's details page.
2. **Given** multiple owners exist whose last names start with "F", **When** a user searches for owners with the last name "F", **Then** a list of owners is displayed.
3. **Given** multiple owners exist, **When** a user searches for owners with an empty last name (or whitespace only), **Then** all owners are displayed.

---

### User Story 2 - Add New Pet to an Owner (Priority: P2)

As a clinic staff member, I want to add a new pet to an existing owner's record so that I can track all of their animals.

**Why this priority**: This is a key feature for managing an owner's complete pet portfolio.

**Independent Test**: Can be fully tested by selecting an owner, navigating to the add pet form, filling in pet details, and verifying the new pet appears in the owner's pet list.

**Acceptance Scenarios**:

1. **Given** an existing owner, **When** the user navigates to the "Add Pet" form for that owner, **Then** the form displays fields for pet name, birth date, and pet type.
2. **Given** the "Add Pet" form is filled with valid pet details (name, birth date, selected pet type), **When** the user submits the form, **Then** the new pet is associated with the owner and displayed in their pet list.

---

### User Story 3 - Update Pet Information (Priority: P3)

As a clinic staff member, I want to update an existing pet's information (e.g., name) so that the records are always accurate.

**Why this priority**: Maintaining accurate pet information is crucial for proper care and record-keeping.

**Independent Test**: Can be fully tested by selecting a pet, editing its name, saving the changes, and verifying the updated name is displayed.

**Acceptance Scenarios**:

1. **Given** an existing pet belonging to an owner, **When** the user navigates to the "Edit Pet" form for that pet, **Then** the form displays the current pet details.
2. **Given** the "Edit Pet" form is used to change the pet's name, **When** the user submits the form, **Then** the pet's name is updated in the system.

---

### Edge Cases

- What happens when an owner is created/updated with a blank address? → Validation error.
- What happens when an owner is created/updated with a blank city? → Validation error.
- What happens when an owner is created/updated with an invalid telephone format (not 10 digits)? → Validation error.
- How does the system handle an attempt to access or modify an owner with a non-existent ID? → `IllegalArgumentException` is thrown.
- What happens when a pet is created/updated with a blank name? → Validation error.
- How does the system handle pet creation/update without selecting a pet type? → Validation error.
- What happens when a pet is created/updated without providing a birth date? → Validation error.
- How does the system handle an attempt to add a pet with a name that already exists for the same owner? → Validation error.
- What happens when a visit is created with a date that is not in the future? → Validation error.
- How does the system handle an attempt to create a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` is thrown.
- What happens when searching for owners with a last name that yields no results? → Validation error indicating "not found".
- How does the system handle navigating to the "/oups" endpoint? → A `RuntimeException` is thrown, showcasing exception handling.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new pets for an owner.
- **FR-002**: System MUST allow updating an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD display a form for creating or updating pet details.
- **FR-005**: System SHOULD provide a list of available pet types for selection.
- **FR-006**: System MUST allow searching for owners by last name.
- **FR-007**: System MUST display a list of owners when a partial last name search is performed.
- **FR-008**: System MUST display all owners when a search with an empty last name is performed.
- **FR-009**: System MUST validate owner information (address, city, telephone) during creation or update.
- **FR-010**: System MUST handle non-existent owner IDs gracefully by throwing an `IllegalArgumentException`.
- **FR-011**: System MUST handle non-existent pet IDs for an owner gracefully by throwing an `IllegalArgumentException`.
- **FR-012**: System MUST display a user-friendly message when no owners are found for a given search.
- **FR-013**: System MUST demonstrate exception handling by throwing a `RuntimeException` on the "/oups" endpoint.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual owner of pets, including their contact information (address, city, telephone) and a list of their associated pets.
- **Pet**: Represents an individual animal owned by a person, including its birth date, type, and a history of visits.
- **PetType**: Represents the classification of a pet (e.g., Cat, Dog, Hamster).
- **Visit**: Represents a record of a pet's visit to the clinic, including the date of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find an owner by their last name in under 3 seconds.
- **SC-002**: Adding a new pet to an owner takes less than 5 seconds.
- **SC-003**: Updating a pet's name is reflected in the system within 2 seconds.
- **SC-004**: 95% of owner and pet data validation errors are clearly communicated to the user.
- **SC-005**: The system successfully handles 100 concurrent requests for owner searches without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing authentication mechanisms if any are present (though not explicitly detailed in the provided context).
- Data persistence will be handled by an underlying data store (e.g., a database), as implied by the entity definitions.
- The "spring-petclinic" project structure and conventions will be followed.
- Error messages for validation failures will be user-friendly and informative.
- The 10-digit telephone pattern is a reasonable default for the target region.
- Future visits are not explicitly restricted, but validation errors for invalid dates will be implemented.