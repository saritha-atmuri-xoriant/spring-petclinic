# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `006-owners-spring-petclinic`

**Created**: 2026-03-19

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly access their details and manage their pets.

**Why this priority**: This is a core functionality for managing existing clients and is essential for day-to-day operations.

**Independent Test**: Can be fully tested by entering a known last name in the search form and verifying that the correct owner's details are displayed.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists in the system,
   **When** a user searches for owners with the last name "Franklin",
   **Then** the system redirects to the owner's details page for "Franklin".
2. **Given** multiple owners exist with the last name "Smith",
   **When** a user searches for owners with the last name "Smith",
   **Then** the system displays a list of all owners with the last name "Smith".
3. **Given** no owners exist with the last name "NonExistent",
   **When** a user searches for owners with the last name "NonExistent",
   **Then** the system displays an error message indicating no owners were found.

---

### User Story 2 - Create a New Owner (Priority: P2)

As a new user, I want to register as a pet owner by providing my contact information so that I can add my pets to the clinic's system.

**Why this priority**: This enables new users to onboard and utilize the clinic's services.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying that the owner is created and their details page is displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form,
   **When** they submit a valid owner form with all required fields filled correctly (first name, last name, address, city, telephone),
   **Then** the owner is created, a "New Owner Created" success message is displayed, and the user is redirected to the owner's detail page.

---

### User Story 3 - Update an Existing Owner (Priority: P2)

As a clinic staff member, I want to update an existing owner's contact information so that the records are accurate.

**Why this priority**: Maintaining accurate owner information is crucial for communication and record-keeping.

**Independent Test**: Can be fully tested by navigating to an owner's details, editing their information, and verifying the changes are saved.

**Acceptance Scenarios**:

1. **Given** an existing owner is selected,
   **When** the user updates the owner's address and city and submits the form,
   **Then** the owner's contact information is updated successfully.

---

### User Story 4 - Add a New Pet for an Owner (Priority: P3)

As a pet owner, I want to add a new pet to my profile so that I can track its visits and health records.

**Why this priority**: This allows owners to manage their pets within the system.

**Independent Test**: Can be fully tested by navigating to an owner's details, initiating the "Add Pet" process, filling in pet details, and verifying the pet is associated with the owner.

**Acceptance Scenarios**:

1. **Given** an existing owner is selected,
   **When** the user adds a new pet with a valid name, birth date, and type,
   **Then** the new pet is successfully associated with the owner.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to find or edit an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Owner Not Found During Find**: Searching for an owner by last name yields no results → validation error "notFound" for lastName.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error "required".
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error "required".
- **Invalid Pet Birth Date Format**: Pet creation/update with a birth date that does not match the expected format → validation error "typeMismatch".
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error "duplicate".
- **Invalid Visit Date**: Submitting a visit with a date that is not in the future → validation error "typeMismatch.visitDate".
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet ID that does not exist for the specified owner → `IllegalArgumentException` is thrown.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow searching for owners by last name.
- **FR-005**: System SHOULD allow viewing a specific owner's details, including their pets.
- **FR-006**: System MUST allow the creation of a new owner with valid contact information.
- **FR-007**: System MUST allow the update of an existing owner's contact information.
- **FR-008**: System MUST display appropriate error messages for invalid owner data during creation or update.
- **FR-009**: System MUST display appropriate error messages when an owner is not found by last name.
- **FR-010**: System MUST allow adding visits for a pet.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including address, city, and telephone. Has a one-to-many relationship with `Pet`.
- **Pet**: Represents a pet, including birth date and type. Has a many-to-one relationship with `PetType` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the type of a pet (e.g., cat, dog).
- **Visit**: Represents a visit to the clinic for a pet, including a date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation is completed successfully for 95% of valid submissions within 10 seconds.
- **SC-003**: Owner information updates are reflected immediately upon saving.
- **SC-004**: The system correctly displays all pets associated with an owner.
- **SC-005**: Validation errors for owner and pet data are displayed clearly to the user within 2 seconds of submission.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms (if any) are handled separately and are not part of this feature's scope.
- The primary users for owner management are clinic staff.
- Data retention policies for owner and pet information are handled by a separate system or are based on industry standards for veterinary clinics.