# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find owners by last name (Priority: P1)

Given owners exist in the system, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for navigating and managing pet owners within the clinic. It's essential for day-to-day operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list of owners. Delivers immediate value for finding existing clients.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** a user searches for owners with the last name prefix "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** there are no owners with the last name "Xyz", **When** a user searches for owners with the last name prefix "Xyz", **Then** a message indicating "No owners found" is displayed.

---

### User Story 2 - Create a new owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: Onboarding new clients is a fundamental business process for any clinic.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying that the owner is created and their details page is displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the "New Owner" form, **When** they enter valid first name, last name, address, city, telephone, and select a pet type, **Then** the owner is successfully created, and the user is redirected to the newly created owner's details page.

---

### User Story 3 - View owner list (Priority: P2)

Given owners exist in the system, When a user navigates to the owners list page, Then all owners are displayed.

**Why this priority**: Provides an overview of all registered owners, useful for administrative tasks and general reference.

**Independent Test**: Can be fully tested by navigating to the owners list page and verifying that all existing owners are displayed.

**Acceptance Scenarios**:

1. **Given** there are 5 owners in the system, **When** a user navigates to the "Owners" list page, **Then** all 5 owners are displayed in a list.

---

### User Story 4 - Add a new pet for an existing owner (Priority: P2)

Given an owner exists in the system, When a user navigates to the owner's details page and initiates adding a new pet, Then they can provide pet details and save the new pet.

**Why this priority**: Essential for managing the pets associated with each owner.

**Independent Test**: Can be tested by selecting an existing owner, navigating to their details, and successfully adding a new pet with valid information.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" exists, **When** the user navigates to John Doe's details page and adds a new pet named "Buddy" of type "Dog" with a birth date, **Then** the pet "Buddy" is successfully associated with John Doe.

---

### User Story 5 - Update an existing pet's information (Priority: P3)

Given a pet exists for an owner, When a user navigates to the pet's details and initiates an update, Then they can modify and save the pet's information.

**Why this priority**: Allows for correction of errors or updating of pet details as needed.

**Independent Test**: Can be tested by selecting an existing pet, modifying a field (e.g., name), and verifying the update.

**Acceptance Scenarios**:

1. **Given** a pet named "Max" of type "Dog" exists for owner "Jane Smith", **When** the user updates the pet's name to "Maximilian", **Then** the pet's name is updated to "Maximilian" on the owner's details page.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error "required".
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error "required".
- **Invalid Pet Birth Date Format**: Pet creation/update with a birth date in an incorrect format (e.g., "2015/02/12") → validation error "typeMismatch".
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error "duplicate".
- **Invalid Visit Date**: Visit submission with a date that is not in the future → validation error "typeMismatch.visitDate".
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` is thrown.
- **Owner Not Found During Find**: Searching for an owner by last name that yields no results → validation error "notFound" on the `lastName` field.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow searching for owners by last name.
- **FR-005**: System SHOULD display a list of pets associated with an owner.
- **FR-006**: System MUST allow the creation of a new owner.
- **FR-007**: System MUST allow the update of an existing owner's details.
- **FR-008**: System MUST display a list of all owners.
- **FR-009**: System MUST validate owner information during creation or update.
- **FR-010**: System MUST allow viewing an owner's details, including their associated pets.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Attributes include first name, last name, address, city, and telephone number. Has a one-to-many relationship with `Pet`.
- **Pet**: Represents a pet belonging to an owner. Attributes include name, birth date, and type. Has a many-to-one relationship with `Owner` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the type of pet (e.g., Cat, Dog). Attributes include name.
- **Visit**: Represents a visit for a pet. Attributes include date and description. Has a many-to-one relationship with `Pet`.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 2 seconds.
- **SC-002**: New owner creation is completed successfully for 99% of valid submissions.
- **SC-003**: The owner list page loads and displays all owners within 3 seconds.
- **SC-004**: Adding a new pet to an owner is completed successfully for 98% of valid submissions.
- **SC-005**: Updating pet information is reflected immediately on the owner's details page.

## Assumptions

- Users have stable internet connectivity.
- The system will be used by clinic staff with appropriate permissions.
- Data validation rules are clearly defined and enforced as per the business rules.
- The system will be deployed in an environment where database persistence is available.
- The user interface for managing owners and pets will be intuitive and user-friendly.