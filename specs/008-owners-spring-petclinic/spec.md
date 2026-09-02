# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `008-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for managing and accessing owner information, essential for day-to-day operations.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and verifying redirection to the correct owner's detail page.

**Acceptance Scenarios**:

1. **Given** an owner named "George Franklin" exists in the system, **When** a user searches for owners with the last name "Franklin", **Then** the system displays the details for George Franklin.
2. **Given** multiple owners with the last name "Smith" exist, **When** a user searches for owners with the last name "Smith", **Then** the system displays a list of all owners with the last name "Smith".

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and the user is redirected to the owner's list.

**Why this priority**: The ability to add new owners is fundamental to growing the pet clinic's customer base.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting the form, and verifying redirection to the owner list page with the new owner present.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" page, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and submit the form, **Then** the new owner is successfully created and the user is redirected to the "Owners" list page.

---

### User Story 3 - Handle Invalid Owner Creation (Priority: P2)

Given a user is on the new owner form, When they submit an invalid owner form, Then an error message is displayed and the form is re-displayed.

**Why this priority**: Ensures data integrity and provides immediate feedback to users, improving the user experience.

**Independent Test**: Can be fully tested by navigating to the new owner form, intentionally leaving a required field blank or entering invalid data (e.g., incorrect phone format), submitting the form, and verifying that appropriate error messages are displayed and the form remains visible.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" page, **When** they leave the "Last Name" field blank and submit the form, **Then** an error message "Last name must not be blank" is displayed next to the "Last Name" field, and the form remains on the page.
2. **Given** a user is on the "Add Owner" page, **When** they enter "123" for the "Telephone" field and submit the form, **Then** an error message indicating an invalid telephone format is displayed, and the form remains on the page.

---

### User Story 4 - Update an Existing Owner (Priority: P2)

Given an existing owner's details are displayed, When a user modifies and submits the owner's information, Then the owner's details are updated.

**Why this priority**: Allows for maintaining accurate and up-to-date owner information.

**Independent Test**: Can be fully tested by finding an existing owner, navigating to their edit page, changing a field (e.g., telephone number), submitting the changes, and verifying that the owner's details page reflects the updated information.

**Acceptance Scenarios**:

1. **Given** an existing owner's details are displayed, **When** the user updates the "Telephone" field to a valid 10-digit number and submits the form, **Then** the owner's telephone number is updated, and the updated details are displayed.

---

### User Story 5 - Add a New Pet for an Owner (Priority: P3)

Given an owner's details are displayed, When a user adds a new pet for that owner, Then the new pet is associated with the owner.

**Why this priority**: Essential for managing the pets associated with each owner.

**Independent Test**: Can be fully tested by navigating to an owner's detail page, initiating the process to add a new pet, filling in the required pet details (name, birth date, type), and verifying that the new pet appears in the owner's pet list.

**Acceptance Scenarios**:

1. **Given** an owner's details are displayed, **When** the user adds a new pet with a valid name, birth date, and selects a pet type, **Then** the new pet is successfully added to the owner's record.

---

### User Story 6 - Add a New Visit for a Pet (Priority: P3)

Given a pet's details are displayed, When a user adds a new visit for that pet, Then the new visit is recorded for the pet.

**Why this priority**: Crucial for tracking the medical history and appointments of pets.

**Independent Test**: Can be fully tested by navigating to a pet's detail page, initiating the process to add a new visit, entering a valid visit date and description, and verifying that the new visit appears in the pet's visit history.

**Acceptance Scenarios**:

1. **Given** a pet's details are displayed, **When** the user adds a new visit with a valid date and description, **Then** the new visit is successfully recorded for the pet.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **No Owners Found**: Searching for owners with a last name that yields no results → error message "not found" is added to the `lastName` field.
- **Blank Pet Name**: Creating or updating a pet with a blank name → validation error "required".
- **Missing Pet Type**: Creating or updating a pet without selecting a pet type → validation error "required".
- **Invalid Pet Birth Date Format**: Creating or updating a pet with a birth date in an incorrect format (e.g., "2015/02/12") → validation error "typeMismatch".
- **Duplicate Pet Name for Same Owner**: Attempting to save a pet with a name that already exists for the same owner → validation error "duplicate".
- **Invalid Visit Date**: Booking a visit with a date that is not in the future → validation error "typeMismatch.visitDate".
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet that does not exist for a given owner → `IllegalArgumentException` is thrown.
- **Exception Trigger**: Accessing the `/oups` endpoint → `RuntimeException` is thrown, leading to an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow searching for owners by last name.
- **FR-005**: System SHOULD allow adding new visits for a pet.
- **FR-006**: System MUST allow the creation of a new owner.
- **FR-007**: System MUST allow the update of an existing owner's information.
- **FR-008**: System MUST validate owner information during creation or update.
- **FR-009**: System MUST display a list of all owners.
- **FR-010**: System MUST display the details of a specific owner.
- **FR-011**: System MUST display the pets associated with an owner.
- **FR-012**: System MUST display the visits associated with a pet.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include first name, last name, address, city, telephone, and a collection of associated pets.
- **Pet**: Represents a pet belonging to an owner. Key attributes include name, birth date, type, and a collection of associated visits.
- **PetType**: Represents the type of pet (e.g., Cat, Dog). Key attributes include name.
- **Visit**: Represents a veterinary visit for a pet. Key attributes include date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created with valid data in under 1 minute.
- **SC-003**: Pet information can be updated successfully with a 99% success rate.
- **SC-004**: New visits can be added for a pet in under 2 minutes.
- **SC-005**: The system supports up to 50 concurrent users browsing owner lists without performance degradation.
- **SC-006**: 95% of invalid owner form submissions result in clear, actionable error messages.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms (if any) will be handled by other modules.
- Data persistence will be managed by the persistence layer, and data integrity will be maintained through database constraints and application-level validation.
- The "owners" module is a standalone feature and does not have complex external dependencies beyond basic data persistence and validation.
- The telephone number format `\d{10}` is the standard for all owners.
- Pet names are unique within an owner.
- Visit dates must be in the future.
- The `/oups` endpoint is intended for testing exception handling and should result in a server error.