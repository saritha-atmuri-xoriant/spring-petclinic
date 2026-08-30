# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `[###-owner-management]`

**Created**: 2026-03-19

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners (Priority: P1)

Given an owner with a known last name exists, When a user searches for owners using that last name, Then the system displays a list of owners matching the last name, or redirects to the owner's details page if only one match is found.

**Why this priority**: This is a core functionality for accessing and managing owner information, essential for day-to-day operations of the clinic.

**Independent Test**: Can be fully tested by searching for existing owners by last name and verifying the displayed results or redirection.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists, **When** a user searches for owners with the last name "Franklin", **Then** the system displays the owner's details page.
2. **Given** multiple owners with the last name "Smith" exist, **When** a user searches for owners with the last name "Smith", **Then** the system displays a list of all owners named "Smith".
3. **Given** no owners exist with the last name "NonExistent", **When** a user searches for owners with the last name "NonExistent", **Then** an appropriate "not found" message is displayed.

---

### User Story 2 - Create New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form with all required fields populated correctly, Then the owner is created, and the user is redirected to the owner's details page or a confirmation page.

**Why this priority**: This is fundamental to onboarding new clients and their pets into the system.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying successful creation and redirection.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form (first name, last name, address, city, telephone), **Then** the owner is created and the user is redirected to the owner's details page.
2. **Given** a user is on the new owner form, **When** they submit an invalid owner form (e.g., blank last name), **Then** the form is redisplayed with clear error messages indicating the validation failures.

---

### User Story 3 - Update Existing Owner (Priority: P2)

Given a user is viewing an existing owner's details, When they choose to edit the owner's information and submit a valid updated form, Then the owner's details are updated, and the user is redirected to the updated owner's details page.

**Why this priority**: Allows for maintaining accurate and up-to-date information for existing clients.

**Independent Test**: Can be fully tested by editing an existing owner's details with valid data and verifying the updates.

**Acceptance Scenarios**:

1. **Given** a user is viewing an owner's details, **When** they edit the owner's telephone number and submit the form, **Then** the owner's telephone number is updated, and the updated details are displayed.
2. **Given** a user is viewing an owner's details, **When** they attempt to update the owner's address with a blank value, **Then** the form is redisplayed with an error message for the address field.

---

### User Story 4 - Add New Pet to Owner (Priority: P2)

Given a user is viewing an owner's details, When they choose to add a new pet for that owner and submit a valid pet form, Then the pet is created and associated with the owner, and the owner's pet list is updated.

**Why this priority**: Essential for managing the pets associated with each owner.

**Independent Test**: Can be fully tested by adding a new pet to an existing owner and verifying its appearance in the owner's pet list.

**Acceptance Scenarios**:

1. **Given** a user is viewing an owner's details, **When** they add a new pet with a valid name, birth date, and select a pet type, **Then** the pet is successfully created and linked to the owner.
2. **Given** a user is viewing an owner's details, **When** they attempt to add a new pet with a blank name, **Then** the form is redisplayed with an error message for the pet name.

---

### User Story 5 - Update Existing Pet Information (Priority: P3)

Given a user is viewing an owner's pets, When they choose to edit a specific pet's information and submit a valid updated form, Then the pet's details are updated, and the updated pet information is displayed.

**Why this priority**: Allows for correcting or updating information about a pet.

**Independent Test**: Can be fully tested by editing an existing pet's details and verifying the updates.

**Acceptance Scenarios**:

1. **Given** a user is viewing an owner's pets, **When** they edit a pet's birth date and submit the form, **Then** the pet's birth date is updated, and the updated details are displayed.
2. **Given** a user is viewing an owner's pets, **When** they attempt to update a pet's name to a duplicate name for the same owner, **Then** the form is redisplayed with a "duplicate" error message.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error "required".
- **Blank Last Name**: Owner creation/update with a blank last name → validation error "required".
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error "required".
- **Blank City**: Owner creation/update with a blank city → validation error "required".
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist in the database → `IllegalArgumentException` is thrown and handled gracefully with a "not found" message.
- **No Owners Found**: Searching for owners with a last name that does not match any records → error message "not found" is added to the `lastName` field.
- **Blank Pet Name**: Creating or updating a pet with a blank name → validation error "required".
- **Missing Pet Type**: Creating or updating a pet without selecting a pet type → validation error "required".
- **Duplicate Pet Name for Same Owner**: Attempting to save a pet with a name that already exists for the same owner → validation error "duplicate".
- **Invalid Pet Birth Date Format**: Creating or updating a pet with a birth date in an incorrect format (e.g., "2015/02/12") → validation error "typeMismatch".
- **Blank Pet Birth Date**: Creating or updating a pet with a null birth date → validation error "required".
- **Invalid Visit Date**: Booking a visit with a date that is not in the future → validation error "visitDate must be in the future".
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` is thrown and handled gracefully.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow the updating of existing owner information.
- **FR-003**: System MUST allow searching for owners by last name.
- **FR-004**: System MUST display owner details upon successful search or creation/update.
- **FR-005**: System MUST validate owner data (first name, last name, address, city, telephone) during creation and update.
- **FR-006**: System MUST allow the creation of new pets for an owner.
- **FR-007**: System MUST allow the updating of existing pet information.
- **FR-008**: System MUST validate pet data (name, birth date, pet type) during creation or update.
- **FR-009**: System SHOULD provide a list of available pet types for selection when creating or updating a pet.
- **FR-010**: System SHOULD handle cases where an owner is not found when attempting to manage their pets or visits.
- **FR-011**: System MUST allow the creation of new visits for a pet.
- **FR-012**: System MUST validate visit data (date, description) during creation.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (name, address, city, telephone) and a collection of associated pets.
- **Pet**: Represents a pet, including its name, birth date, type, and associated owner and visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a veterinary visit for a pet, including the date and a description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created with valid data in under 1 minute.
- **SC-003**: Existing owner information can be updated in under 45 seconds.
- **SC-004**: New pets can be added to an owner in under 1 minute.
- **SC-005**: 95% of form submissions for owner, pet, or visit data are valid on the first attempt.
- **SC-006**: The system correctly handles and displays "not found" scenarios for owners and pets.

## Assumptions

- Users have stable internet connectivity.
- The system will use a relational database for persistence.
- Standard web browser functionality is assumed for user interaction.
- The application will be deployed in an environment where Spring Boot applications are supported.
- Existing authentication mechanisms (if any) will be leveraged for user access control, though this specification focuses on the owner management functionality itself.
- The `Person` class is a base for `Owner` and includes common fields like first and last name.
- The `NamedEntity` class is a base for `Pet` and `PetType`, providing a `name` field.
- The `BaseEntity` class is a base for `Visit`, providing an ID.
- Telephone numbers are expected to be 10 digits without any special characters or formatting.
- Pet birth dates are expected in `yyyy-MM-dd` format.
- Visit dates are expected in `yyyy-MM-dd` format and must be in the future.