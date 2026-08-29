# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `014-owners-spring-petclinic`

**Created**: 2026-08-29

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a list of owners exists, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for navigating and managing existing owners, essential for day-to-day operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list matches the expected owners, delivering the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for "Sm", **Then** owners "Smith" and "Smythe" are displayed.
2. **Given** there are no owners with the last name "Davis", **When** the user searches for "Davis", **Then** a message indicating no owners were found is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: Essential for onboarding new clients and expanding the pet clinic's customer base.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and confirming redirection to the newly created owner's detail page, delivering the ability to add new clients.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and submit the form, **Then** the owner is successfully created and the user is redirected to the owner's detail page.
2. **Given** the user is on the "Add Owner" page, **When** they attempt to submit the form with a blank first name, **Then** a validation error message is displayed for the first name field, and the owner is not created.

---

### User Story 3 - View Owner Details (Priority: P2)

Given an owner exists, When the user navigates to the owner's details page, Then all owner attributes are displayed.

**Why this priority**: Allows users to access and review all relevant information about a specific owner and their pets.

**Independent Test**: Can be fully tested by selecting an owner from a list and verifying all their associated details (personal information, pets, visits) are displayed correctly, delivering visibility into owner and pet data.

**Acceptance Scenarios**:

1. **Given** an owner named "John Doe" exists with associated pets and visits, **When** the user navigates to John Doe's owner details page, **Then** the owner's first name, last name, address, city, telephone number, and a list of their pets with their respective visit history are displayed.

---

### User Story 4 - Update Owner Information (Priority: P2)

Given a user is viewing an owner's details, When they edit and submit valid owner information, Then the owner's details are updated.

**Why this priority**: Allows for maintaining accurate and up-to-date owner information.

**Independent Test**: Can be fully tested by editing an existing owner's details and confirming the changes are saved and reflected on the owner's detail page, delivering the ability to correct and update client information.

**Acceptance Scenarios**:

1. **Given** the user is on an owner's detail page, **When** they click the "Edit" button, modify the telephone number, and submit the changes, **Then** the owner's telephone number is updated, and the detail page reflects the new number.
2. **Given** the user is on an owner's detail page, **When** they click the "Edit" button and attempt to submit the form with an invalid telephone number format, **Then** a validation error message is displayed for the telephone field, and the owner's information is not updated.

---

### User Story 5 - Add a New Pet for an Owner (Priority: P2)

Given a user is viewing an owner's details, When they add a new pet with valid information, Then the new pet is associated with the owner.

**Why this priority**: Enables comprehensive management of an owner's pets within the system.

**Independent Test**: Can be fully tested by navigating to an owner's detail page, adding a new pet with valid data, and confirming the pet appears in the owner's pet list, delivering the ability to register new pets for existing clients.

**Acceptance Scenarios**:

1. **Given** the user is on an owner's detail page, **When** they click "Add New Pet", fill in the pet's name, birth date, and select a pet type, and submit the form, **Then** the new pet is successfully added to the owner's record and displayed in the pet list.
2. **Given** the user is on an owner's detail page, **When** they click "Add New Pet" and attempt to submit the form with a blank pet name, **Then** a validation error message is displayed for the pet name field, and the pet is not added.

---

### User Story 6 - View Pet Details and Visits (Priority: P3)

Given a pet exists for an owner, When the user views the pet's details, Then the pet's information and associated visits are displayed.

**Why this priority**: Provides a consolidated view of a pet's history and medical records.

**Independent Test**: Can be fully tested by selecting a pet from an owner's detail page and verifying its information and all associated visit records are displayed, delivering access to a pet's complete history.

**Acceptance Scenarios**:

1. **Given** a pet named "Buddy" exists for an owner with several visits recorded, **When** the user navigates to Buddy's detail page, **Then** Buddy's name, birth date, type, and a chronological list of all his visits are displayed.

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
- **Non-existent Owner ID for Visit**: Attempting to add a visit for a pet belonging to a non-existent owner → `IllegalArgumentException` is thrown.
- **Non-existent Pet ID for Visit**: Attempting to add a visit for a non-existent pet belonging to an owner → `IllegalArgumentException` is thrown.
- **Blank Pet Name Validation**: Pet validation with a blank name → `errors.hasFieldErrors("name")` is true.
- **Null Pet Type Validation**: Pet validation with a null pet type → `errors.hasFieldErrors("type")` is true.
- **Null Pet Birth Date Validation**: Pet validation with a null birth date → `errors.hasFieldErrors("birthDate")` is true.
- **Owner Form Submission Restrictions**: When creating or updating an owner, the address and telephone fields are disallowed from being set directly via form submission.
- **Visit Form Submission Restrictions**: When creating or updating a visit, the ID field is disallowed from being set directly via form submission.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow searching for owners by last name.
- **FR-005**: System SHOULD display a list of pets associated with an owner.
- **FR-006**: System MUST allow the creation of a new owner.
- **FR-007**: System MUST allow the update of an existing owner's information.
- **FR-008**: System MUST display an owner's details, including their pets and visits.
- **FR-009**: System MUST allow the creation of a new visit for an existing pet.
- **FR-010**: System MUST validate owner information during creation or update.
- **FR-011**: System MUST validate visit information during creation or update.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details like name, address, city, and telephone number. It is associated with multiple pets.
- **Pet**: Represents a pet, including its name, birth date, and type. It is associated with an owner and multiple visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a record of a pet's visit to the clinic, including the date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 2 seconds.
- **SC-002**: New owners can be created with valid data in under 1 minute.
- **SC-003**: Owner details, including pets and visits, are displayed within 3 seconds of navigation.
- **SC-004**: New pets can be added to an owner's record in under 1.5 minutes.
- **SC-005**: 95% of form submissions for owner and pet data are successful on the first attempt due to effective validation.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms will be leveraged if applicable to user roles (though not explicitly detailed in this feature description).
- The system will use a relational database for persistence.
- Standard date and time formats will be used for user input and display.
- The system will provide user-friendly error messages for validation failures.
- The primary language for the application is English.
- The system will be deployed in a standard web server environment.
- The telephone number format `\d{10}` is a strict requirement for all owners.
- Pet names must be unique per owner.
- Visit dates must be in the future relative to the submission date.