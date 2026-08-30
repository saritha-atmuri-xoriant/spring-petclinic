# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `032-owners-spring-petclinic`

**Created**: 2026-03-19

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given owners exist in the system, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for day-to-day operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the displayed results, delivering the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for "Sm", **Then** owners "Smith" and "Smythe" are displayed.
2. **Given** there are no owners with the last name "Davis", **When** the user searches for "Davis", **Then** no owners are displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: This is a fundamental operation for adding new clients to the clinic.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and submitting it, verifying the owner is created and their details page is shown.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Submit", **Then** the new owner is saved, and the user is redirected to the details page for that newly created owner.

---

### User Story 3 - Handle Duplicate Pet Name Violation (Priority: P2)

Given an owner has existing pets, When a user attempts to add a new pet with a name that already exists for that owner, Then an error message indicating the duplicate name is displayed, and the form is re-rendered.

**Why this priority**: Prevents data integrity issues and provides clear feedback to the user.

**Independent Test**: Can be tested by adding a pet to an owner, then attempting to add another pet with the same name for that same owner, verifying the error message.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" has a pet named "Buddy", **When** the user attempts to add another pet for "John Doe" and enters "Buddy" as the pet's name, **Then** an error message "The pet name must be unique for a given owner" is displayed, and the pet creation form is re-rendered with the entered data.

---

### User Story 4 - Update Existing Owner Information (Priority: P2)

Given an owner exists in the system, When a user edits the owner's details and submits valid changes, Then the owner's information is updated.

**Why this priority**: Allows for correction of errors or updating of client information.

**Independent Test**: Can be tested by selecting an existing owner, modifying their details, and saving the changes, verifying the updated information is displayed.

**Acceptance Scenarios**:

1. **Given** an owner "Jane Smith" exists with address "123 Main St", **When** the user navigates to edit Jane Smith's details, changes the address to "456 Oak Ave", and submits the form, **Then** the owner's address is updated to "456 Oak Ave".

---

### User Story 5 - Add a New Pet to an Existing Owner (Priority: P3)

Given an owner exists in the system, When a user adds a new pet for that owner with valid details, Then the new pet is associated with the owner.

**Why this priority**: Essential for managing the pets associated with each owner.

**Independent Test**: Can be tested by selecting an owner, navigating to add a pet, filling in valid pet details, and saving, verifying the pet is linked to the owner.

**Acceptance Scenarios**:

1. **Given** owner "Alice Wonderland" exists, **When** the user adds a new pet named "Fluffy" of type "Cat" with a birth date, **Then** "Fluffy" is successfully added and associated with "Alice Wonderland".

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or access an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation with a missing pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to save a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Visit submission with a date that is not in the future → validation error.
- **Non-existent Owner ID for Visit**: Attempting to create a visit for an owner ID that does not exist → `IllegalArgumentException` is thrown.
- **Non-existent Pet ID for Visit**: Attempting to create a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` is thrown.
- **Crash Endpoint**: Accessing the `/oups` endpoint → `RuntimeException` is thrown, resulting in an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow finding owners by their last name.
- **FR-005**: System SHOULD allow inserting a new owner.
- **FR-006**: System MUST allow updating an existing owner's details.
- **FR-007**: System MUST enforce that owner's first name is not blank.
- **FR-008**: System MUST enforce that owner's last name is not blank.
- **FR-009**: System MUST enforce that owner's address is not blank.
- **FR-010**: System MUST enforce that owner's city is not blank.
- **FR-011**: System MUST enforce that owner's telephone number is exactly 10 digits.
- **FR-012**: System MUST enforce that a pet's name is not blank.
- **FR-013**: System MUST enforce that a pet's name is unique for a given owner.
- **FR-014**: System MUST allow the creation of new visits for a pet.
- **FR-015**: System MUST display a list of owners when searching by last name prefix.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their contact information (address, city, telephone) and associated pets.
- **Pet**: Represents a pet, including its birth date and type, associated with an owner and having a history of visits.
- **PetType**: Represents the classification of a pet (e.g., Cat, Dog).
- **Visit**: Represents a record of a pet's visit, including the date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully find owners by last name prefix in under 2 seconds.
- **SC-002**: New owners can be created and their details page viewed within 3 minutes of form submission.
- **SC-003**: 95% of users successfully add a new pet to an existing owner on their first attempt.
- **SC-004**: Validation errors for owner and pet data are displayed clearly and immediately upon form submission.
- **SC-005**: The system supports managing up to 1000 owners and their associated pets without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Standard date formats will be used for pet birth dates and visit dates.
- The application will be deployed in an environment where Spring Boot auto-configuration is enabled.
- Existing user authentication mechanisms (if any) are outside the scope of this feature.
- The primary user for managing owners and pets is a clinic staff member.