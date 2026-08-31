# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `056-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing existing clients and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search bar and verifying the displayed list of owners.

**Acceptance Scenarios**:

1. **Given** there are owners in the system with last names "Smith", "Smythe", and "Jones", **When** a user searches for owners with the last name prefix "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** there are no owners with the last name "Davis", **When** a user searches for owners with the last name prefix "Dav", **Then** a message indicating no owners were found is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a new user, I want to create a new owner profile so that I can register my pets with the clinic.

**Why this priority**: This is crucial for onboarding new clients and expanding the clinic's customer base.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying redirection to the owner's detail page.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they enter valid first name, last name, address, city, and telephone number, and click "Save", **Then** the owner is created and the user is redirected to the newly created owner's detail page.
2. **Given** a user is on the "Add Owner" form, **When** they leave the "First Name" field blank and click "Save", **Then** a validation error message for the first name is displayed, and the form remains on the "Add Owner" page.

---

### User Story 3 - Add a New Pet to an Existing Owner (Priority: P2)

As a clinic staff member, I want to add a new pet to an existing owner's profile so that I can record their animals.

**Why this priority**: This is important for maintaining accurate pet records for existing clients.

**Independent Test**: Can be fully tested by navigating to an owner's detail page, clicking "Add New Pet", filling out the pet form with valid data, and verifying the pet is added to the owner's list.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" exists with no pets, **When** a user navigates to John Doe's profile, clicks "Add New Pet", and submits a valid pet form (name, birth date, type), **Then** the new pet is successfully added to John Doe's profile.
2. **Given** an owner "Jane Smith" exists with a pet named "Buddy", **When** a user attempts to add another pet named "Buddy" for Jane Smith, **Then** a validation error message indicating a duplicate pet name is displayed, and the pet form remains on the page.

---

### User Story 4 - Add a Visit for a Pet (Priority: P2)

As a clinic staff member, I want to add a new visit record for a pet so that I can track their medical history.

**Why this priority**: Essential for maintaining a complete medical history for each pet.

**Independent Test**: Can be fully tested by navigating to a pet's detail page, clicking "Add New Visit", filling out the visit form with valid data, and verifying the visit is recorded.

**Acceptance Scenarios**:

1. **Given** a pet "Max" exists for owner "John Doe", **When** a user navigates to Max's profile, clicks "Add New Visit", and submits a valid visit form (date, description), **Then** the new visit is successfully recorded for Max.
2. **Given** a pet "Max" exists for owner "John Doe", **When** a user attempts to submit a visit with an invalid date (e.g., in the past), **Then** a validation error message for the visit date is displayed, and the visit form remains on the page.

---

### User Story 5 - Update an Existing Owner's Information (Priority: P3)

As a clinic staff member, I want to update an existing owner's contact information so that the records are always current.

**Why this priority**: Ensures accurate contact information for communication with owners.

**Independent Test**: Can be fully tested by navigating to an owner's detail page, clicking "Edit Owner", modifying a field, saving, and verifying the change.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" exists with address "123 Main St", **When** a user edits John Doe's profile and changes the address to "456 Oak Ave", and clicks "Save", **Then** the owner's address is updated to "456 Oak Ave".
2. **Given** an owner "Jane Smith" exists, **When** a user attempts to edit Jane Smith's profile and enters an invalid telephone number (e.g., "123"), **Then** a validation error message for the telephone number is displayed, and the edit form remains on the page.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` regex → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or access an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Visit submission with a date that is not in the future → validation error.
- **Non-existent Owner ID for Visit**: Attempting to add a visit for an owner ID that does not exist → `IllegalArgumentException` is thrown.
- **Non-existent Pet ID for Visit**: Attempting to add a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` is thrown.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow finding owners by their last name.
- **FR-005**: System SHOULD allow adding a new visit for a pet.
- **FR-006**: System MUST allow the creation of a new owner.
- **FR-007**: System MUST allow the update of an existing owner's address, city, and telephone number.
- **FR-008**: System MUST validate owner information (first name, last name, address, city, telephone) during creation or update.
- **FR-009**: System MUST allow viewing an owner's details, including their pets and visits.
- **FR-010**: System MUST allow viewing a pet's details, including its visits.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (name, address, city, telephone) and a collection of associated pets.
- **Pet**: Represents a pet, including its name, birth date, type, and a collection of associated visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a medical visit for a pet, including the date and a description of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 2 seconds.
- **SC-002**: New owner creation and redirection to their detail page completes in under 3 seconds.
- **SC-003**: Adding a new pet to an owner's profile is confirmed within 2 seconds.
- **SC-004**: Adding a visit for a pet is confirmed within 2 seconds.
- **SC-005**: 95% of owner and pet data updates are successfully saved and reflected within 2 seconds.
- **SC-006**: Validation errors for owner and pet forms are displayed immediately upon submission of invalid data.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed by clinic staff and new clients.
- The existing `Person` class is suitable for owner details.
- The `NamedEntity` and `BaseEntity` classes are appropriate for pet and visit entities respectively.
- A standard relational database will be used for persistence.
- The telephone number format validation (`\d{10}`) is sufficient for current needs.
- The date format for pet birth dates and visit dates is `yyyy-MM-dd`.
- The system will be deployed within a standard web application environment.
- Internationalization (i18n) for user-facing strings will be handled as per project constitution.