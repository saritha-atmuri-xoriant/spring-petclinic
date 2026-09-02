# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `007-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for navigating the application and finding specific owner information.

**Independent Test**: Can be fully tested by entering "Franklin" in the last name search field and verifying redirection to the correct owner's detail page.

**Acceptance Scenarios**:

1. **Given** an owner named "John Franklin" exists, **When** a user searches for owners with the last name "Franklin", **Then** the system displays the details page for John Franklin.

---

### User Story 2 - Find Owners with Partial Last Name Match (Priority: P2)

Given multiple owners whose last names start with "Frank" exist, When a user searches for owners with the last name "Frank", Then a list of all matching owners is displayed.

**Why this priority**: This allows for flexible searching and discovery of owners when the exact last name is not known.

**Independent Test**: Can be fully tested by entering "Frank" in the last name search field and verifying that all owners whose last names start with "Frank" are displayed in a list.

**Acceptance Scenarios**:

1. **Given** owners "John Franklin" and "Jane Frank" exist, **When** a user searches for owners with the last name "Frank", **Then** a list containing both "John Franklin" and "Jane Frank" is displayed.

---

### User Story 3 - Handle Empty Last Name Search (Priority: P3)

Given multiple owners exist, When a user searches for owners with an empty or whitespace-only last name, Then all owners are displayed in the owner list.

**Why this priority**: This ensures a graceful fallback for users who do not provide a search term, providing a comprehensive view of all owners.

**Independent Test**: Can be fully tested by leaving the last name search field empty and submitting the search, verifying that all owners are displayed.

**Acceptance Scenarios**:

1. **Given** multiple owners exist, **When** a user searches for owners with an empty last name, **Then** all owners are displayed in the owner list.

---

### User Story 4 - Create New Owner (Priority: P1)

Given a user wants to add a new pet owner, When the user fills out the new owner form with valid details and submits it, Then a new owner record is created and the user is redirected to the owner's details page.

**Why this priority**: This is a fundamental operation for managing the pet clinic's client base.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying that the owner is created and their details page is displayed.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** the user enters valid first name, last name, address, city, and telephone, and submits the form, **Then** a new owner record is created and the user is redirected to the newly created owner's details page.

---

### User Story 5 - Edit Existing Owner (Priority: P2)

Given an existing owner's details are displayed, When the user modifies the owner's information (e.g., address, phone number) and submits the changes, Then the owner's record is updated and the updated details are displayed.

**Why this priority**: Allows for maintaining accurate owner information over time.

**Independent Test**: Can be fully tested by navigating to an owner's details, editing a field, submitting, and verifying the change.

**Acceptance Scenarios**:

1. **Given** an existing owner's details are displayed, **When** the user changes the owner's telephone number and submits, **Then** the owner's record is updated with the new telephone number and the updated details are displayed.

---

### User Story 6 - Add New Pet to Owner (Priority: P1)

Given an owner's details are displayed, When the user chooses to add a new pet, fills out the pet details (name, birth date, type), and submits, Then the new pet is associated with the owner and displayed in the owner's pet list.

**Why this priority**: Essential for managing the pets associated with each owner.

**Independent Test**: Can be fully tested by navigating to an owner's details, adding a new pet with valid information, and verifying its appearance in the pet list.

**Acceptance Scenarios**:

1. **Given** an owner's details are displayed, **When** the user adds a new pet named "Buddy" with a birth date and selects "Dog" as the type, **Then** "Buddy" appears in the owner's list of pets.

---

### User Story 7 - Edit Existing Pet (Priority: P2)

Given a pet's details are displayed within an owner's profile, When the user modifies the pet's information (e.g., name, birth date) and submits, Then the pet's record is updated and the updated details are displayed.

**Why this priority**: Allows for correcting or updating pet information.

**Independent Test**: Can be fully tested by navigating to a pet's details within an owner's profile, editing a field, submitting, and verifying the change.

**Acceptance Scenarios**:

1. **Given** a pet named "Buddy" is listed under an owner, **When** the user edits Buddy's name to "Buddy Jr." and submits, **Then** the pet's name is updated to "Buddy Jr." in the owner's pet list.

---

### User Story 8 - Add New Visit to Pet (Priority: P1)

Given a pet's details are displayed within an owner's profile, When the user chooses to add a new visit, provides a date and description, and submits, Then the new visit is associated with the pet and displayed in the pet's visit history.

**Why this priority**: Crucial for tracking the medical history of pets.

**Independent Test**: Can be fully tested by navigating to a pet's details, adding a new visit with a date and description, and verifying its appearance in the visit history.

**Acceptance Scenarios**:

1. **Given** a pet named "Buddy" is listed under an owner, **When** the user adds a visit on "2026-09-05" with the description "Routine check-up", **Then** the visit appears in Buddy's visit history.

---

### User Story 9 - Edit Existing Visit (Priority: P2)

Given a visit's details are displayed within a pet's history, When the user modifies the visit's information (e.g., description) and submits, Then the visit's record is updated and the updated details are displayed.

**Why this priority**: Allows for correcting or updating visit records.

**Independent Test**: Can be fully tested by navigating to a visit's details, editing a field, submitting, and verifying the change.

**Acceptance Scenarios**:

1. **Given** a visit for "Buddy" on "2026-09-05" with description "Routine check-up" exists, **When** the user edits the description to "Annual check-up" and submits, **Then** the visit's description is updated to "Annual check-up".

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
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Visit creation with a date that is not in the future → validation error.
- **Non-existent Owner ID for Pet Visit**: Attempting to create a visit for a pet belonging to a non-existent owner → `IllegalArgumentException` is thrown.
- **Non-existent Pet ID for Visit**: Attempting to create a visit for a pet that does not exist for a given owner → `IllegalArgumentException` is thrown.
- **Concurrency Issue with Duplicate Pet Name**: Multiple concurrent requests to add a pet with the same name to the same owner → only one request should succeed, others should fail.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow updating an existing owner's details (address, city, telephone).
- **FR-003**: System MUST allow searching for owners by last name, supporting exact and partial matches.
- **FR-004**: System MUST display all owners when a search for an empty last name is performed.
- **FR-005**: System MUST allow the creation of new pets for an owner.
- **FR-006**: System MUST allow updating an existing pet's name and birth date.
- **FR-007**: System MUST allow adding new visits for a pet, including date and description.
- **FR-008**: System MUST allow updating an existing visit's description.
- **FR-009**: System MUST validate owner information during creation or update, enforcing non-blank fields for first name, last name, address, and city, and a 10-digit format for telephone.
- **FR-010**: System MUST validate pet information during creation or update, enforcing non-blank name and requiring a valid pet type and birth date.
- **FR-011**: System MUST validate visit information during creation, requiring a valid date and description.
- **FR-012**: System MUST prevent duplicate pet names for the same owner.
- **FR-013**: System MUST display a form for creating or updating owner details.
- **FR-014**: System MUST display a form for creating or updating pet details.
- **FR-015**: System MUST display a form for creating or updating visit details.
- **FR-016**: System MUST populate a list of available pet types for selection during pet creation/update.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (address, city, telephone) and a collection of associated pets.
- **Pet**: Represents a pet, including its name, birth date, type, and a history of visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a medical visit for a pet, including the date and a description of the service provided.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 2 seconds.
- **SC-002**: New owner creation and redirection to their details page completes in under 3 seconds.
- **SC-003**: Adding a new pet to an owner and seeing it reflected in the list completes in under 3 seconds.
- **SC-004**: Adding a new visit to a pet and seeing it in the visit history completes in under 3 seconds.
- **SC-005**: 99% of owner, pet, and visit creation/update operations succeed without validation errors when valid data is provided.
- **SC-006**: All validation errors for owner, pet, and visit data are clearly communicated to the user.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- The system will use a relational database for persistence.
- Standard date formats will be used for pet birth dates and visit dates.
- The list of pet types is predefined and managed separately.
- Error messages will be user-friendly and informative.
- The system will handle concurrent requests for adding pets to the same owner gracefully, ensuring data integrity.