# Feature Specification: Owner Management

**Feature Branch**: `005-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given owners exist in the system, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for navigating and managing existing pet owners, essential for day-to-day operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** a user searches for owners with the last name prefix "Sm", **Then** the system displays owners "Smith" and "Smythe".
2. **Given** there are no owners with the last name "Davis", **When** a user searches for owners with the last name prefix "Dav", **Then** the system displays a message indicating no owners were found.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the owner creation form, When they submit a valid owner form, Then a new owner is created and added to the system.

**Why this priority**: Essential for onboarding new pet owners into the system.

**Independent Test**: Can be fully tested by filling out the owner creation form with valid data and verifying the new owner appears in the owner list. Delivers the ability to add new pet owners.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" page, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and submit the form, **Then** the new owner is successfully created and displayed in the owner list.

---

### User Story 3 - View Owner List (Priority: P2)

Given owners exist in the system, When a user navigates to the owners list page, Then all owners are displayed, paginated.

**Why this priority**: Provides an overview of all registered owners, important for administrative tasks and general system visibility.

**Independent Test**: Can be fully tested by navigating to the owner list page and verifying that all existing owners are displayed, with pagination controls if the list is long. Delivers a comprehensive view of all owners.

**Acceptance Scenarios**:

1. **Given** there are more than 10 owners in the system, **When** a user navigates to the owner list page, **Then** the first 10 owners are displayed, along with pagination controls to navigate to subsequent pages.
2. **Given** there are fewer than 10 owners in the system, **When** a user navigates to the owner list page, **Then** all owners are displayed without pagination controls.

---

### User Story 4 - Edit an Existing Owner (Priority: P2)

Given an existing owner is selected, When a user updates their information and submits the form, Then the owner's details are updated in the system.

**Why this priority**: Allows for maintaining accurate owner information as it changes.

**Independent Test**: Can be fully tested by selecting an owner, modifying a field, and verifying the change is saved. Delivers the ability to update owner details.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" exists, **When** a user navigates to edit "John Doe", changes their telephone number, and submits the form, **Then** the owner's telephone number is updated.

---

### User Story 5 - Create a New Pet for an Owner (Priority: P3)

Given an existing owner is selected, When a user adds a new pet for that owner, Then the pet is associated with the owner.

**Why this priority**: Enables owners to register their pets within the system.

**Independent Test**: Can be fully tested by selecting an owner, adding a new pet with valid details, and verifying the pet is listed under that owner. Delivers the ability to register pets.

**Acceptance Scenarios**:

1. **Given** owner "Jane Smith" exists, **When** a user navigates to "Jane Smith"'s profile, adds a new pet named "Buddy" of type "Dog" with a birth date, and submits, **Then** "Buddy" is listed as a pet belonging to "Jane Smith".

---

### Edge Cases

- What happens when an owner's first name is blank during creation or update? → Validation error.
- What happens when an owner's last name is blank during creation or update? → Validation error.
- What happens when an owner's telephone number does not match the 10-digit pattern during creation or update? → Validation error.
- What happens when an owner's address is blank during creation or update? → Validation error.
- What happens when an owner's city is blank during creation or update? → Validation error.
- How does the system handle an attempt to edit or view an owner with a non-existent ID? → `IllegalArgumentException` is thrown.
- What happens when a pet's name is blank during creation or update? → Validation error "required".
- What happens when a pet type is not specified during pet creation or update? → Validation error "required".
- How does the system handle an attempt to add a pet with a name that already exists for the same owner? → Validation error "duplicate".
- What happens when a pet's birth date is in an incorrect format during creation or update? → Validation error "typeMismatch".
- How does the `PetValidator` flag a blank pet name? → Flags as an error.
- How does the `PetValidator` flag a null pet type? → Flags as an error.
- How does the `PetValidator` flag a null pet birth date? → Flags as an error.
- What happens when a visit date is submitted that is not in the future? → Validation error "typeMismatch.visitDate".
- How does the system handle an attempt to create a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` is thrown.
- How does the system handle an attempt to create a visit for an owner ID that does not exist? → `IllegalArgumentException` is thrown.
- How does the system handle an attempt to create or update a pet for an owner ID that does not exist? → `IllegalArgumentException` is thrown.
- How does the system handle an attempt to edit an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when searching for owners by last name results in no owners found? → Validation error "notFound" on `lastName`.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for a given owner.
- **FR-002**: System MUST allow the updating of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow the retrieval of all pet types for populating forms.
- **FR-005**: System SHOULD handle data integrity violations when saving pet information.
- **FR-006**: System MUST allow searching for owners by their last name prefix.
- **FR-007**: System MUST allow the creation of new owners with valid address, city, and telephone information.
- **FR-008**: System MUST allow the viewing of a list of all owners, with pagination.
- **FR-009**: System MUST allow the editing of existing owner details.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Includes fields for address, city, and telephone. Can have multiple pets.
- **Pet**: Represents a pet belonging to an owner. Includes fields for birth date and type. Can have multiple visits.
- **PetType**: Represents the type of a pet (e.g., cat, dog).
- **Visit**: Represents a visit to the vet for a pet. Includes a date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully find owners by last name prefix in under 2 seconds.
- **SC-002**: New owners can be created with valid data in under 1 minute.
- **SC-003**: The owner list page loads and displays paginated results within 3 seconds.
- **SC-004**: 95% of pet creation/update operations complete successfully with valid data.
- **SC-005**: Support tickets related to incorrect owner information are reduced by 30% within one quarter of release.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms will be leveraged if applicable to owner management actions.
- Data integrity for pet types will be managed separately or pre-populated.
- The primary users of this feature are clinic staff responsible for managing owner and pet information.