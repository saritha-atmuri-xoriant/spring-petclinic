# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-09-04

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for navigating the application and accessing owner information.

**Independent Test**: Can be fully tested by searching for an existing owner's last name and verifying the correct details page is displayed.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists in the system, **When** a user navigates to the "Find Owners" page and enters "Franklin" in the last name field, **Then** the system displays the details for the owner named Franklin.
2. **Given** no owners exist with the last name "Smith", **When** a user navigates to the "Find Owners" page and enters "Smith" in the last name field, **Then** an error message "not found" is displayed next to the last name field.

---

### User Story 2 - Create a New Owner (Priority: P2)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and a success message is displayed.

**Why this priority**: Adding new owners is essential for populating the system with data.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and confirming the owner is added to the system and a success message is shown.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they enter valid details for first name, last name, address, city, and telephone number, and submit the form, **Then** the new owner is successfully created and displayed in the system, and a success message is shown.

---

### User Story 3 - Handle Invalid Owner Creation (Priority: P3)

Given a user is on the new owner form, When they submit an invalid owner form, Then the system displays an error message and returns to the form.

**Why this priority**: Ensures data integrity by preventing invalid owner data from being saved.

**Independent Test**: Can be fully tested by attempting to submit the new owner form with invalid data (e.g., blank fields, incorrect phone format) and verifying error messages are displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they submit the form with a blank address, **Then** a validation error message is displayed for the address field, and the form remains open.
2. **Given** a user is on the "Add Owner" form, **When** they submit the form with a telephone number that is not 10 digits, **Then** a validation error message is displayed for the telephone number field, and the form remains open.

---

### User Story 4 - Create a New Pet for an Existing Owner (Priority: P1)

Given an existing owner, When a user adds a new pet for that owner with valid details, Then the pet is successfully created and associated with the owner.

**Why this priority**: Managing pets is a core function of the pet clinic.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to the add pet form, entering valid pet details, and confirming the pet is associated with the owner.

**Acceptance Scenarios**:

1. **Given** an existing owner exists, **When** a user navigates to add a pet for that owner and provides a valid pet name, birth date, and selects a pet type, **Then** the pet is created and linked to the owner.

---

### User Story 5 - Update an Existing Pet's Name (Priority: P2)

Given an existing pet, When a user updates the pet's name to a valid, unique name for that owner, Then the pet's name is updated successfully.

**Why this priority**: Allows for correction of pet names and ensures data accuracy.

**Independent Test**: Can be fully tested by selecting an existing pet, changing its name to a valid and unique name for the owner, and confirming the update.

**Acceptance Scenarios**:

1. **Given** an existing pet associated with an owner, **When** the user edits the pet's details and changes the name to a new, valid, and unique name for that owner, **Then** the pet's name is updated in the system.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → validation error.
- **Non-existent Owner ID**: Attempting to access or modify an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error.
- **Missing Pet Birth Date**: Pet creation/update without providing a birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Visit creation/update with a date that is not after the current date → validation error.
- **Non-existent Pet ID for Owner**: Attempting to create a visit for a pet that does not exist for a given owner → `IllegalArgumentException` is thrown.
- **Owner Not Found During Find**: Searching for owners with a last name that yields no results → error message "not found" is added to the owner's lastName field.
- **Concurrent Pet Creation**: Multiple concurrent requests to create a pet for the same owner → only one request should succeed, others should fail due to duplicate name validation.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow updating an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow finding owners by last name.
- **FR-005**: System SHOULD allow retrieving an owner by their ID and display their pets.
- **FR-006**: System MUST enforce that owner's first name is not blank.
- **FR-007**: System MUST enforce that owner's last name is not blank.
- **FR-008**: System MUST enforce that owner's address is not blank.
- **FR-009**: System MUST enforce that owner's city is not blank.
- **FR-010**: System MUST enforce that owner's telephone number is exactly 10 digits.
- **FR-011**: System MUST enforce that pet's name is not blank.
- **FR-012**: System MUST enforce that a pet's name is unique for a given owner.
- **FR-013**: System MUST enforce that visit description is not blank.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (name, address, city, phone) and a collection of associated pets.
- **Pet**: Represents a pet, including its name, birth date, type, and associated owner and visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a clinic visit for a pet, including the date and a description of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 2 seconds.
- **SC-002**: New owner creation is completed within 5 seconds for valid data.
- **SC-003**: Validation errors for owner creation are displayed to the user immediately upon submission of invalid data.
- **SC-004**: New pet creation for an existing owner is completed within 3 seconds.
- **SC-005**: 95% of pet updates (including name changes) are successful.
- **SC-006**: The system correctly identifies and prevents duplicate pet names for the same owner.

## Assumptions

- Users have stable internet connectivity.
- The application will be deployed in an environment where database persistence is available.
- Standard web browser functionality is assumed for user interaction.
- The existing `Person` class is suitable for owner details.
- The `NamedEntity` and `BaseEntity` classes are correctly implemented and available.
- The date format for pet birth dates and visit dates will be consistently handled as yyyy-MM-dd.
- The telephone number validation regex is correctly implemented.
- The system will handle concurrent pet creation attempts by ensuring only one succeeds and others fail gracefully due to duplicate name validation.