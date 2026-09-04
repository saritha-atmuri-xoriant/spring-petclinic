# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-09-04

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

A user can search for owners by their last name. If an owner with that last name exists, the system displays their details.

**Why this priority**: This is a core functionality for navigating and managing owner information, essential for basic application use.

**Independent Test**: Can be fully tested by entering a known owner's last name in the search field and verifying that their details page is displayed.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists, **When** a user searches for owners with the last name "Franklin", **Then** the system redirects to the owner's details page for "Franklin".
2. **Given** no owner with the last name "Smith" exists, **When** a user searches for owners with the last name "Smith", **Then** the system displays a "No owners found" message.

---

### User Story 2 - Create a New Owner (Priority: P1)

A user can submit a valid owner form to create a new owner record in the system.

**Why this priority**: Creating new owners is fundamental to populating the system with data and enabling other owner-related features.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying that the owner is created and visible in the owner list.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form (including first name, last name, address, city, and telephone), **Then** the owner is created and the user is redirected to the owner's details page.
2. **Given** a user is on the new owner form, **When** they submit the form with a blank first name, **Then** a validation error is displayed for the first name field, and the owner is not created.

---

### User Story 3 - View a List of Owners (Priority: P2)

A user can view a list of all owners currently in the system.

**Why this priority**: This provides an overview of the data and is necessary for selecting owners for further actions like viewing details or editing.

**Independent Test**: Can be fully tested by navigating to the owners list page and verifying that all existing owners are displayed.

**Acceptance Scenarios**:

1. **Given** there are multiple owners in the system (e.g., Franklin, Davis, Rodriguez), **When** a user navigates to the owners list page, **Then** all owners are displayed, showing at least their first and last names.

---

### User Story 4 - Update an Existing Owner (Priority: P2)

A user can edit the details of an existing owner.

**Why this priority**: Allows for correction of data and maintenance of owner information.

**Independent Test**: Can be fully tested by selecting an owner from the list, editing a field (e.g., telephone number), saving the changes, and verifying the update.

**Acceptance Scenarios**:

1. **Given** an owner exists with a specific telephone number, **When** a user navigates to the owner's edit page, changes the telephone number to a valid new number, and saves, **Then** the owner's telephone number is updated.
2. **Given** an owner exists, **When** a user navigates to the owner's edit page and attempts to save with a blank city, **Then** a validation error is displayed for the city field, and the owner is not updated.

---

### User Story 5 - Add a New Pet to an Owner (Priority: P3)

An owner can have new pets added to their record.

**Why this priority**: Essential for managing the full lifecycle of an owner's relationship with their pets.

**Independent Test**: Can be fully tested by selecting an owner, navigating to their pet management section, and adding a new pet with valid details.

**Acceptance Scenarios**:

1. **Given** an owner exists, **When** the user navigates to the owner's details page and selects to add a new pet, filling in a valid pet name, birth date, and selecting a pet type, **Then** the new pet is associated with the owner.
2. **Given** an owner exists, **When** the user attempts to add a pet with a blank name, **Then** a validation error is displayed for the pet name, and the pet is not added.

---

### User Story 6 - View and Add Visits for a Pet (Priority: P3)

Users can view existing visits for a pet and add new visits.

**Why this priority**: Tracks the history and future appointments for a pet.

**Independent Test**: Can be fully tested by selecting a pet, viewing its visit history, and adding a new visit with a valid date.

**Acceptance Scenarios**:

1. **Given** a pet has existing visits, **When** the user navigates to the pet's details page, **Then** all associated visits are displayed with their dates.
2. **Given** a pet exists, **When** the user navigates to the pet's details page and adds a new visit with a valid future date, **Then** the new visit is recorded for the pet.

---

### Edge Cases

- What happens when an owner is created/updated with a telephone number that is not exactly 10 digits? → Validation error.
- How does the system handle an attempt to edit or view an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when a pet is created/updated with a name that already exists for the same owner? → Validation error.
- How does the system handle a visit creation with a date that is not in the future? → Validation error.
- What happens when a user searches for an owner by last name that does not exist in the database? → Validation error "notFound" on the `lastName` field.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow searching for owners by last name.
- **FR-003**: System MUST display owner details when found by last name.
- **FR-004**: System MUST allow updating an existing owner's details.
- **FR-005**: System MUST allow the creation of new pets for an owner, including name, birth date, and pet type.
- **FR-006**: System MUST allow updating an existing pet's name.
- **FR-007**: System SHOULD validate pet data during creation or update.
- **FR-008**: System SHOULD display a form for creating or updating pet information.
- **FR-009**: System SHOULD populate a dropdown list with available pet types during pet creation/update.
- **FR-010**: System MUST allow viewing existing visits for a pet.
- **FR-011**: System MUST allow adding new visits for a pet with a date.
- **FR-012**: System MUST validate owner's telephone number to be exactly 10 digits.
- **FR-013**: System MUST validate that pet's name is unique for a given owner.
- **FR-014**: System MUST validate that visit description is not blank.
- **FR-015**: System MUST validate that pet's name is not blank.
- **FR-016**: System MUST validate that owner's first name is not blank.
- **FR-017**: System MUST validate that owner's last name is not blank.
- **FR-018**: System MUST validate that owner's address is not blank.
- **FR-019**: System MUST validate that owner's city is not blank.
- **FR-020**: System MUST validate that visit date is not blank.
- **FR-021**: System MUST validate that visit date is in the future.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual owner of pets. Key attributes include first name, last name, address, city, telephone, and a collection of associated pets.
- **Pet**: Represents an animal owned by an owner. Key attributes include name, birth date, type, and a collection of associated visits.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog). Key attribute is its name.
- **Visit**: Represents a veterinary visit for a pet. Key attributes include date and a description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find and view an owner's details within 5 seconds of searching by last name.
- **SC-002**: New owners can be successfully created with all required fields in under 1 minute.
- **SC-003**: 95% of pet creation/update operations complete successfully with valid data.
- **SC-004**: The system supports displaying a list of up to 100 owners without significant performance degradation.
- **SC-005**: All validation errors for owner and pet data are displayed clearly to the user.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Standard date and time formats will be used for user input.
- The underlying database is available and functional.
- Pet types (e.g., Cat, Dog) are pre-defined and available for selection.