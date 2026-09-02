# Feature Specification: Owner Management

**Feature Branch**: `[###-owner-management]`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find owners by last name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for retrieving existing owner information, essential for day-to-day operations.

**Independent Test**: Can be fully tested by searching for a known owner's last name and verifying the correct owner details page is displayed.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists in the system, **When** a user searches for owners using "Franklin" as the last name, **Then** the system displays the details of the owner named "Franklin".
2. **Given** multiple owners exist with the last name "Smith", **When** a user searches for owners using "Smith" as the last name, **Then** the system displays a list of all owners with the last name "Smith".

---

### User Story 2 - Create a new owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and a success message is displayed.

**Why this priority**: Essential for onboarding new clients into the pet clinic system.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and confirming the owner is added to the system and a success message is shown.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they enter valid details for first name, last name, address, city, and telephone, and submit the form, **Then** a new owner record is created in the system, and a confirmation message is displayed.

---

### User Story 3 - Update an existing owner (Priority: P2)

Given an existing owner's details are displayed, When a user modifies and saves the owner's information, Then the owner's details are updated in the system.

**Why this priority**: Allows for maintaining accurate and up-to-date owner information.

**Independent Test**: Can be fully tested by selecting an existing owner, modifying a field (e.g., telephone number), saving the changes, and verifying the updated information is displayed.

**Acceptance Scenarios**:

1. **Given** an owner's details are displayed, **When** a user edits the owner's address and saves the changes, **Then** the owner's address is updated in the system.

---

### User Story 4 - Handle invalid owner creation (Priority: P2)

Given a user is on the new owner form, When they submit an invalid owner form, Then the system displays an error message and returns to the owner creation form.

**Why this priority**: Ensures data integrity by preventing invalid data from being saved.

**Independent Test**: Can be fully tested by submitting the new owner form with invalid data (e.g., blank last name) and verifying that an error message is shown and the form remains editable.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they submit the form with a blank last name, **Then** the system displays a validation error message indicating the last name is required, and the form remains on the page for correction.
2. **Given** a user is on the "Add Owner" form, **When** they submit the form with a telephone number that is not 10 digits, **Then** the system displays a validation error message indicating an invalid telephone format, and the form remains on the page for correction.

---

### User Story 5 - View owner's pets (Priority: P3)

Given an owner has associated pets, When a user views the owner's details, Then the system displays a list of the owner's pets.

**Why this priority**: Provides a comprehensive view of the owner's relationship with their pets.

**Independent Test**: Can be fully tested by selecting an owner known to have pets and verifying that their pets are listed on the owner's detail page.

**Acceptance Scenarios**:

1. **Given** an owner named "John Doe" has two pets, "Buddy" and "Lucy", **When** a user views the details for "John Doe", **Then** the system displays "Buddy" and "Lucy" as associated pets.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **No Owners Found**: Searching for owners with a last name that yields no results → system displays a "not found" error message.
- **Blank Pet Name**: Creating or updating a pet with a blank name → validation error "required".
- **Missing Pet Type**: Creating a pet without specifying a pet type → validation error "required".
- **Invalid Pet Birth Date Format**: Creating or updating a pet with a birth date in an incorrect format (e.g., "2015/02/12") → validation error "typeMismatch".
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error "duplicate".
- **Invalid Visit Date**: Booking a visit with a date that is not in the future → validation error "typeMismatch.visitDate".
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet that does not exist for the specified owner → `IllegalArgumentException` is thrown.
- **Exception Trigger**: Accessing the `/oups` endpoint → a `RuntimeException` is thrown, indicating an expected exception scenario.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the updating of an existing owner's information (address, city, telephone).
- **FR-003**: System MUST allow owners to be searched by last name.
- **FR-004**: System MUST display a list of pets associated with an owner when viewing their details.
- **FR-005**: System MUST validate owner information during creation and update, enforcing non-blank fields for first name, last name, address, and city, and a 10-digit format for telephone.
- **FR-006**: System MUST display appropriate error messages for invalid owner data.
- **FR-007**: System MUST handle cases where no owners are found for a given search term.
- **FR-008**: System MUST allow the creation of a new pet for an existing owner.
- **FR-009**: System MUST allow the updating of an existing pet's name.
- **FR-010**: System SHOULD validate pet information during creation or update.
- **FR-011**: System SHOULD display a list of pets associated with an owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (first name, last name, address, city, telephone) and a collection of associated pets.
- **Pet**: Represents a pet belonging to an owner, including its name, birth date, and type.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a scheduled visit for a pet to the clinic.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully create a new owner record in under 1 minute.
- **SC-002**: Owner searches by last name return results within 2 seconds.
- **SC-003**: 95% of owner data updates are completed successfully without errors.
- **SC-004**: The system prevents the creation of owners with incomplete mandatory fields.
- **SC-005**: The system displays a clear "no results found" message when an owner search yields no matches.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing mechanisms for displaying lists and detail views.
- Data validation rules are applied consistently across creation and update operations.
- The system will provide user-friendly error messages for all validation failures.
- The primary focus is on managing owner information and their associated pets.