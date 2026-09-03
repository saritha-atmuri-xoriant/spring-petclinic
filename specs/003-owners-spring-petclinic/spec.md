# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `003-owners-spring-petclinic`

**Created**: 2026-09-03

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system displays the owner's details page.

**Why this priority**: This is a core functionality for navigating the application and finding existing pet owners.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and verifying that the details for the "Franklin" owner are displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the "Find Owners" page, **When** they enter "Franklin" in the "Last name" field and click "Search", **Then** the system displays the details for the owner named "Franklin".
2. **Given** a user is on the "Find Owners" page, **When** they enter a last name that does not exist and click "Search", **Then** the system displays a "notFound" error message for the last name field.

---

### User Story 2 - Create a New Owner (Priority: P2)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and the user is redirected to the owner's details page.

**Why this priority**: Essential for onboarding new clients into the system.

**Independent Test**: Can be fully tested by navigating to the "Add Owner" form, filling in all required fields with valid data, submitting the form, and verifying that the new owner's details page is displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Submit", **Then** the new owner is created and the system redirects to the owner's details page.

---

### User Story 3 - Handle Invalid Owner Creation (Priority: P3)

Given a user is on the new owner form, When they submit an invalid owner form, Then the system displays an error message and returns to the owner creation form.

**Why this priority**: Ensures data integrity and provides feedback to the user.

**Independent Test**: Can be fully tested by navigating to the "Add Owner" form, intentionally leaving a required field blank or entering invalid data (e.g., non-numeric phone number), submitting the form, and verifying that error messages are displayed and the form remains visible.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they leave the "First name" field blank and click "Submit", **Then** the system displays a validation error message for the "First name" field and the form remains visible.
2. **Given** a user is on the "Add Owner" form, **When** they enter a 9-digit number in the "Telephone" field and click "Submit", **Then** the system displays a validation error message for the "Telephone" field and the form remains visible.

---

### User Story 4 - Add a New Pet to an Owner (Priority: P2)

Given an owner exists, When a user navigates to the owner's details page and chooses to add a pet, Then they can enter pet details (name, birth date, type) and save the new pet.

**Why this priority**: Core functionality for managing a pet owner's pets.

**Independent Test**: Can be fully tested by finding an existing owner, navigating to their details, initiating the "Add Pet" process, filling in valid pet details, and saving.

**Acceptance Scenarios**:

1. **Given** an owner exists, **When** the user navigates to the owner's details page and clicks "Add New Pet", **Then** a form is displayed to enter pet details.
2. **Given** the user is on the "Add New Pet" form for an owner, **When** they enter a valid pet name, birth date, and select a pet type, and click "Submit", **Then** the new pet is associated with the owner and displayed on the owner's details page.

---

### User Story 5 - Update an Existing Pet's Name (Priority: P3)

Given a pet exists for an owner, When a user navigates to the pet's details and chooses to edit the name, Then they can update the pet's name and save the changes.

**Why this priority**: Allows for correction of pet names.

**Independent Test**: Can be fully tested by finding an owner, selecting one of their pets, initiating the edit pet process, changing the pet's name, and saving.

**Acceptance Scenarios**:

1. **Given** a pet exists for an owner, **When** the user navigates to the pet's details and clicks "Edit Pet", **Then** the pet's name field is editable.
2. **Given** the user is editing a pet's details, **When** they change the pet's name to a new valid name and click "Submit", **Then** the pet's name is updated and reflected on the owner's details page.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Owner Not Found During Find**: Searching for an owner by last name that yields no results → validation error "notFound" for `lastName`.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error "required".
- **Missing Pet Type**: Pet creation with a missing pet type → validation error "required".
- **Invalid Pet Birth Date Format**: Pet creation/update with a birth date not in the "yyyy-MM-dd" format → validation error "typeMismatch".
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error "duplicate".
- **Invalid Visit Date**: Visit submission with a date that is not in the future → validation error "typeMismatch.visitDate".
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` is thrown.
- **Exception Trigger**: Accessing the `/oups` endpoint → `RuntimeException` is thrown, resulting in an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow searching for owners by last name.
- **FR-003**: System MUST allow updating an existing owner's information (first name, last name, address, city, telephone).
- **FR-004**: System MUST allow the creation of new pets for an owner.
- **FR-005**: System MUST allow updating an existing pet's name.
- **FR-006**: System SHOULD validate owner data during creation or update, enforcing non-blank fields for first name, last name, address, and city, and a 10-digit format for telephone.
- **FR-007**: System SHOULD validate pet data during creation or update, enforcing non-blank names and valid birth dates.
- **FR-008**: System SHOULD populate a list of available pet types when creating or updating a pet.
- **FR-009**: System MUST prevent duplicate pet names for the same owner.
- **FR-010**: System MUST display a form for creating or updating owner information.
- **FR-011**: System MUST display a form for creating or updating pet information.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Attributes include first name, last name, address, city, and telephone number. Can have multiple pets.
- **Pet**: Represents a pet belonging to an owner. Attributes include name, birth date, and type. Can have multiple visits.
- **PetType**: Represents the type of pet (e.g., Cat, Dog). Has a name.
- **Visit**: Represents a visit to the clinic for a pet. Attributes include date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find an owner by last name in under 3 seconds.
- **SC-002**: New owner creation is completed by users in under 2 minutes.
- **SC-003**: 95% of owner and pet data validation errors are clearly displayed to the user upon submission.
- **SC-004**: Users can successfully add a new pet to an existing owner in under 5 minutes.
- **SC-005**: The system supports up to 500 concurrent users browsing owner and pet information without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- Existing authentication mechanisms (if any) are handled separately and are not part of this feature's scope.
- The list of available pet types is managed and provided by the system.
- Data retention policies for owner and pet information are handled by a separate system or are outside the scope of this initial feature.
- Error handling for non-existent owner or pet IDs will result in user-friendly error messages rather than raw exceptions being exposed.