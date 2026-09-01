# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `004-owners-spring-petclinic`

**Created**: 2026-09-01

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for navigating and accessing owner information, essential for basic system usability.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and verifying redirection to the correct owner's detail page. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** an owner named "George Franklin" exists in the system, **When** a user searches for owners with the last name "Franklin", **Then** the system displays the details for "George Franklin".
2. **Given** multiple owners with the last name "Smith" exist, **When** a user searches for owners with the last name "Smith", **Then** the system displays a list of all owners with the last name "Smith".
3. **Given** no owners with the last name "NonExistent" exist, **When** a user searches for owners with the last name "NonExistent", **Then** the system displays a "Owner not found" message.

---

### User Story 2 - Create a New Owner (Priority: P2)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and the user is redirected to the owner's list.

**Why this priority**: Adding new owners is a fundamental operation for populating and managing the pet clinic's client base.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required valid fields, submitting the form, and verifying redirection to the owner list page with the new owner present. Delivers the ability to onboard new clients.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they enter valid details for first name, last name, address, city, and telephone, **Then** the owner is successfully created and the user is redirected to the owner list page.
2. **Given** a user is on the new owner form, **When** they enter valid details and add at least one pet with a valid name and type, **Then** the owner and their pet are successfully created and the user is redirected to the owner list page.

---

### User Story 3 - Handle Invalid Owner Creation (Priority: P3)

Given a user is on the new owner form, When they submit an invalid owner form, Then an error message is displayed and the user remains on the creation form.

**Why this priority**: Ensures data integrity and guides users to correct input, improving the user experience and data quality.

**Independent Test**: Can be fully tested by navigating to the new owner form, intentionally submitting invalid data (e.g., blank address, invalid phone number), and verifying that error messages are displayed and the user remains on the form. Delivers robust data validation.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit the form with a blank address, **Then** an error message indicating "Address must not be blank" is displayed, and the user remains on the form.
2. **Given** a user is on the new owner form, **When** they submit the form with a telephone number that is not 10 digits, **Then** an error message indicating "Invalid telephone number" is displayed, and the user remains on the form.
3. **Given** a user is on the new owner form, **When** they submit the form with a blank last name, **Then** an error message indicating "Last name must not be blank" is displayed, and the user remains on the form.

---

### User Story 4 - Create a New Pet for an Owner (Priority: P1)

Given an existing owner, When a user navigates to the owner's detail page and initiates pet creation, Then the system allows the user to add a new pet with a name, birth date, and type.

**Why this priority**: Managing pets is central to the pet clinic's operations, and adding new pets is a frequent and essential task.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their detail page, initiating the pet creation process, filling in valid pet details, and verifying the pet is associated with the owner. Delivers the ability to register new pets.

**Acceptance Scenarios**:

1. **Given** an existing owner, **When** the user adds a new pet with a valid name, birth date, and selects a pet type, **Then** the pet is successfully created and associated with the owner.
2. **Given** an existing owner, **When** the user attempts to add a pet with a blank name, **Then** a validation error is displayed, and the pet is not created.
3. **Given** an existing owner, **When** the user attempts to add a pet without selecting a pet type, **Then** a validation error is displayed, and the pet is not created.

---

### User Story 5 - Update an Existing Pet's Name (Priority: P2)

Given an existing pet associated with an owner, When a user navigates to the pet's details and initiates an update, Then the system allows the user to change the pet's name.

**Why this priority**: Allows for correction of errors or changes in pet naming conventions, maintaining accurate records.

**Independent Test**: Can be fully tested by selecting an existing pet, navigating to its details, changing the name to a new valid name, and verifying the update. Delivers the ability to correct pet names.

**Acceptance Scenarios**:

1. **Given** an existing pet, **When** the user updates the pet's name to a new valid name, **Then** the pet's name is successfully updated.
2. **Given** an existing pet, **When** the user attempts to update the pet's name to a blank name, **Then** a validation error is displayed, and the name is not updated.
3. **Given** an existing pet, **When** the user attempts to update the pet's name to a name that already exists for the same owner, **Then** a validation error is displayed, and the name is not updated.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → validation error.
- **Non-existent Owner ID**: Attempting to access or modify an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Visit creation/update with a date that is not after the current date → validation error.
- **Non-existent Pet ID for Owner**: Attempting to create a visit for a pet that does not exist for a given owner → `IllegalArgumentException` is thrown.
- **Owner Not Found During Find**: Searching for owners with a last name that yields no results → validation error indicating "not found".
- **Exception Trigger**: Navigating to the `/oups` endpoint → `RuntimeException` is thrown, showcasing exception handling.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new pets for an owner.
- **FR-002**: System MUST allow updating an existing pet's name.
- **FR-003**: System SHOULD validate pet data during creation or update.
- **FR-004**: System SHOULD allow searching for owners by last name.
- **FR-005**: System SHOULD display a list of pets associated with an owner.
- **FR-006**: System MUST disallow the ID field and any fields within the owner object that contain an ID when creating or updating an owner.
- **FR-007**: System MUST disallow the ID field and any fields within the visit object that contain an ID when creating or updating a visit.
- **FR-008**: System MUST enforce that an owner's first name is not blank.
- **FR-009**: System MUST enforce that an owner's last name is not blank.
- **FR-010**: System MUST enforce that an owner's address is not blank.
- **FR-011**: System MUST enforce that an owner's city is not blank.
- **FR-012**: System MUST enforce that an owner's telephone number is exactly 10 digits.
- **FR-013**: System MUST enforce that a pet's name is not blank.
- **FR-014**: System MUST enforce that a pet's name is unique for a given owner.
- **FR-015**: System MUST enforce that a visit's description is not blank.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their contact information (address, city, telephone) and associated pets.
- **Pet**: Represents a pet belonging to an owner, including its name, birth date, and type.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog).
- **Visit**: Represents a veterinary visit for a pet, including the date and a description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully search for and view owner details by last name in under 5 seconds.
- **SC-002**: New owners can be created with all required valid information in under 2 minutes.
- **SC-003**: New pets can be added to an existing owner's profile in under 1 minute.
- **SC-004**: 95% of owner and pet data entries pass validation checks upon submission.
- **SC-005**: The system correctly handles and displays validation errors for invalid input, guiding users to correct data entry.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- The primary database is H2, with support for MySQL and PostgreSQL demonstrated in integration tests.
- Standard web application performance expectations apply for page load times and form submissions.
- User roles and permissions are not explicitly defined in this feature and are assumed to be handled by a separate authentication/authorization mechanism.
- The `PetType` entity will have a predefined set of types available for selection (e.g., Cat, Dog, Bird, etc.).
- The system will use standard date formats for birth dates and visit dates.
- The `Visit` entity will be associated with a `Pet` which is in turn associated with an `Owner`.
- The `owners` module is the primary focus, and other modules of the Spring Petclinic application are assumed to be functional and stable.