# Feature Specification: owners for spring-petclinic

**Feature Branch**: `020-owners-spring-petclinic`

**Created**: 2026-03-19

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given owners exist in the system, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for managing pet clinic data, allowing staff to quickly locate specific owners.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the displayed list against known owner data.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** there are no owners with the last name "Davis", **When** the user searches for "Davis", **Then** an empty list or a "no results found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: Essential for onboarding new clients and their pets into the clinic's system.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying that the owner is created and their details page is shown.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" form, **When** they enter valid first name, last name, address, city, telephone, and submit the form, **Then** the new owner is saved and the user is redirected to the owner's details page.

---

### User Story 3 - View Owner List (Priority: P2)

Given owners exist in the system, When a user navigates to the owners list page, Then all owners are displayed.

**Why this priority**: Provides an overview of all registered owners, useful for administrative tasks and general reference.

**Independent Test**: Can be fully tested by navigating to the owners list page and verifying that all existing owners are displayed.

**Acceptance Scenarios**:

1. **Given** there are 5 owners in the system, **When** the user navigates to the "Owners" list page, **Then** all 5 owners are displayed in a list.

---

### User Story 4 - View Owner Details (Priority: P2)

Given an owner exists in the system, When a user selects an owner from the list or search results, Then the owner's details, including their pets, are displayed.

**Why this priority**: Allows staff to access comprehensive information about a specific owner and their pets.

**Independent Test**: Can be fully tested by selecting an owner from the list and verifying that their personal details and associated pets are shown.

**Acceptance Scenarios**:

1. **Given** an owner named "John Doe" has two pets, "Buddy" (Dog) and "Whiskers" (Cat), **When** the user selects "John Doe" from the owner list, **Then** the owner's details (address, phone, etc.) and a list of their pets ("Buddy", "Whiskers") are displayed.

---

### User Story 5 - Update Owner Information (Priority: P3)

Given a user is viewing an owner's details, When they edit and submit valid updated information, Then the owner's details are updated.

**Why this priority**: Allows for correction of errors or updating of owner contact information.

**Independent Test**: Can be fully tested by editing an owner's details and verifying the changes are saved.

**Acceptance Scenarios**:

1. **Given** an owner's telephone number is "1234567890", **When** the user edits the owner's details and changes the telephone number to "0987654321" and submits, **Then** the owner's telephone number is updated to "0987654321".

---

### User Story 6 - Create a New Pet for an Owner (Priority: P3)

Given a user is viewing an owner's details, When they add a new pet with valid information, Then the pet is associated with the owner.

**Why this priority**: Enables the registration of new pets for existing clients.

**Independent Test**: Can be fully tested by adding a new pet to an existing owner and verifying the association.

**Acceptance Scenarios**:

1. **Given** an owner "Jane Smith" exists, **When** the user adds a new pet named "Fido" (Dog) to "Jane Smith" and submits, **Then** "Fido" is listed as a pet belonging to "Jane Smith".

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error.
- **Missing Pet Birth Date**: Pet creation/update without providing a birth date → validation error.
- **Invalid Pet Birth Date Format**: Pet creation/update with a birth date in an incorrect format (e.g., "2015/02/12") → `typeMismatch` validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error indicating the name is "duplicate".

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for a given owner.
- **FR-002**: System MUST allow the updating of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow searching for owners by last name.
- **FR-005**: System SHOULD display a list of pets associated with an owner.
- **FR-006**: System MUST allow the creation of new owners.
- **FR-007**: System MUST allow the updating of existing owner information.
- **FR-008**: System MUST display a list of all owners.
- **FR-009**: System MUST display the details of a specific owner, including their pets.
- **FR-010**: System MUST validate owner information during creation or update.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual who owns one or more pets. Key attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents an animal owned by an owner. Key attributes include name, birth date, and type. A pet belongs to one owner and can have multiple visits.
- **PetType**: Represents the category of a pet (e.g., Dog, Cat, Hamster). Key attribute is the name of the pet type. A pet type can be associated with multiple pets.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 3 seconds.
- **SC-002**: New owner creation is completed by staff in under 2 minutes.
- **SC-003**: 95% of owner and pet data entries are validated successfully upon submission.
- **SC-004**: Staff can view an owner's details and associated pets within 5 seconds.
- **SC-005**: The system supports up to 50 concurrent users accessing owner and pet information without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed by authorized clinic staff.
- Existing data for owners and pets will be migrated or available.
- The primary language for the application interface is English.
- Standard date and time formats will be used for pet birth dates and visit dates.