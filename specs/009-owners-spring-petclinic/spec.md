# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `[###-owners-for-spring-petclinic]`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given owners exist in the system, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for managing pet owners and is essential for day-to-day operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the displayed list of owners.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for "Sm", **Then** owners "Smith" and "Smythe" are displayed.
2. **Given** there are no owners with the last name "Davis", **When** the user searches for "Davis", **Then** a message indicating "No owners found" is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: This is a fundamental requirement for adding new clients to the clinic.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and confirming the owner is created and their details page is shown.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and submit the form, **Then** the new owner is saved and the user is redirected to the owner's details page.

---

### User Story 3 - View Owner List (Priority: P2)

Given owners exist in the system, When a user navigates to the owners list page, Then all owners are displayed.

**Why this priority**: Provides an overview of all registered owners, useful for administrative tasks and quick reference.

**Independent Test**: Can be fully tested by navigating to the owners list page and verifying that all existing owners are displayed.

**Acceptance Scenarios**:

1. **Given** there are multiple owners registered in the system, **When** the user navigates to the "Owners" page, **Then** a list displaying all registered owners, including their names and basic contact information, is shown.

---

### User Story 4 - Update Existing Owner (Priority: P2)

Given an existing owner is selected, When a user updates their information and saves, Then the owner's details are updated.

**Why this priority**: Allows for maintaining accurate owner information as it changes.

**Independent Test**: Can be fully tested by selecting an owner, modifying their details, saving, and then re-viewing their details to confirm the changes.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" exists with address "123 Main St", **When** the user navigates to John Doe's details, edits the address to "456 Oak Ave", and saves, **Then** John Doe's owner record shows the updated address "456 Oak Ave".

---

### User Story 5 - Add a New Pet to an Owner (Priority: P3)

Given an owner is selected, When a user adds a new pet for that owner, Then the pet is associated with the owner.

**Why this priority**: Essential for managing the pets associated with each owner.

**Independent Test**: Can be fully tested by selecting an owner, navigating to the "Add Pet" section, filling in pet details, and confirming the pet is listed under the owner.

**Acceptance Scenarios**:

1. **Given** owner "Jane Smith" exists, **When** the user navigates to Jane Smith's details, selects "Add Pet", fills in the pet's name, birth date, and type, and saves, **Then** the new pet appears in Jane Smith's list of pets.

---

### User Story 6 - View Pet Details and Visits (Priority: P3)

Given a pet is selected, When a user views the pet's details, Then the pet's information and its visit history are displayed.

**Why this priority**: Allows for tracking a pet's health history and upcoming appointments.

**Independent Test**: Can be fully tested by selecting a pet with existing visits and verifying that both the pet's information and its visit history are displayed.

**Acceptance Scenarios**:

1. **Given** a pet "Buddy" has visits recorded on "2026-01-15" and "2026-03-10", **When** the user navigates to Buddy's details page, **Then** Buddy's name, birth date, type, and the list of visits with their dates and descriptions are displayed.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → validation error.
- **Non-existent Owner ID**: Attempting to edit or access an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation with a missing pet type → validation error.
- **Duplicate Pet Name**: Attempting to create a pet with a name that already exists for the same owner → validation error.
- **Invalid Pet Birth Date**: Pet creation/update with an invalid birth date format → validation error.
- **Blank Pet Birth Date**: Pet creation/update with a blank birth date → validation error.
- **Invalid Visit Date**: Visit creation with a date that is not after the current date → validation error.
- **Non-existent Owner ID for Visit**: Attempting to create a visit for a pet belonging to a non-existent owner → `IllegalArgumentException` is thrown.
- **Non-existent Pet ID for Visit**: Attempting to create a visit for a non-existent pet belonging to an owner → `IllegalArgumentException` is thrown.
- **Owner Not Found during Find**: Searching for owners with a last name that yields no results → validation error indicating "not found".

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for a given owner.
- **FR-002**: System MUST allow the updating of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow searching for owners by last name.
- **FR-005**: System SHOULD display a list of pets associated with an owner.
- **FR-006**: System MUST allow the creation of a new owner.
- **FR-007**: System MUST allow the updating of an existing owner's details (address, city, telephone).
- **FR-008**: System MUST allow viewing a list of all owners.
- **FR-009**: System MUST allow viewing the details of a specific owner, including their associated pets.
- **FR-010**: System MUST allow the creation of a new visit for a specific pet.
- **FR-011**: System MUST allow the updating of an existing visit's details.
- **FR-012**: System MUST allow viewing the visit history for a specific pet.
- **FR-013**: System MUST validate owner information during creation or update.
- **FR-014**: System MUST validate visit information during creation or update.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal contact information and a list of their pets.
- **Pet**: Represents a pet, including its name, birth date, type, and associated visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a veterinary visit for a pet, including the date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully create a new owner in under 1 minute.
- **SC-002**: Users can find owners by last name prefix with results displayed in under 2 seconds.
- **SC-003**: 95% of pet creation/update operations complete successfully with valid data.
- **SC-004**: The system can display a list of 100 owners with associated pets in under 5 seconds.
- **SC-005**: Users can add a new visit for a pet with all required information in under 3 minutes.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing data for owners, pets, and visits will be migrated or available.
- The application will be deployed in an environment where database access is reliable.
- Standard date and time formats will be used for user input and display.