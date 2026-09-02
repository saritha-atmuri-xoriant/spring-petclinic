# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `005-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given owners exist in the system, When a user searches for owners by a last name starting with "Franklin", Then the system displays a list of owners whose last names start with "Franklin" and redirects to the owner's detail page.

**Why this priority**: This is a core functionality for managing pet owners and is essential for day-to-day operations.

**Independent Test**: Can be fully tested by entering "Franklin" into the owner search field and verifying the displayed results and navigation to the owner detail page.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Franklin", "Smith", and "Johnson", **When** a user searches for owners with the last name "Franklin", **Then** only owners with the last name "Franklin" are displayed.
2. **Given** an owner named "John Franklin" exists, **When** a user searches for "Franklin" and clicks on "John Franklin" from the results, **Then** the system navigates to the detail page for John Franklin.

---

### User Story 2 - Create a New Owner (Priority: P2)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and a success message is displayed.

**Why this priority**: Adding new owners is a fundamental requirement for expanding the pet clinic's client base.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting the form, and verifying the owner is listed and a success message is shown.

**Acceptance Scenarios**:

1. **Given** a user is on the "New Owner" form, **When** they enter valid data for first name, last name, address, city, telephone, and email, **Then** the owner is successfully created and the user is redirected to the owner's detail page with a success notification.

---

### User Story 3 - Update an Existing Owner (Priority: P2)

Given a user is viewing an owner's detail page, When they edit the owner's information and submit valid changes, Then the owner's details are updated and a success message is displayed.

**Why this priority**: Allows for maintaining accurate owner information as circumstances change.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their edit form, making a valid change (e.g., updating the phone number), submitting the form, and verifying the updated information on the detail page.

**Acceptance Scenarios**:

1. **Given** a user is on an owner's detail page, **When** they click "Edit Owner", enter a new valid telephone number, and click "Save", **Then** the owner's telephone number is updated, and a success message is displayed.

---

### User Story 4 - Handle Invalid Owner Creation (Priority: P3)

Given a user is on the new owner form, When they submit an invalid owner form (e.g., missing required fields, invalid phone format), Then an error message is displayed and the form is re-rendered with the invalid fields highlighted.

**Why this priority**: Ensures data integrity and guides users to provide correct information.

**Independent Test**: Can be fully tested by attempting to submit the new owner form with missing or invalid data and verifying that appropriate error messages are displayed and the form remains editable.

**Acceptance Scenarios**:

1. **Given** a user is on the "New Owner" form, **When** they leave the "Last Name" field blank and click "Save", **Then** an error message "Last name must not be blank" is displayed, and the form is re-rendered with the "Last Name" field highlighted.
2. **Given** a user is on the "New Owner" form, **When** they enter "123" for the "Telephone" field and click "Save", **Then** an error message "Telephone must be exactly 10 digits" is displayed, and the form is re-rendered with the "Telephone" field highlighted.

---

### Edge Cases

- What happens when an owner's first name is blank? → Validation error.
- What happens when an owner's last name is blank? → Validation error.
- What happens when an owner's address is blank? → Validation error.
- What happens when an owner's city is blank? → Validation error.
- What happens when an owner's telephone number does not match the `\d{10}` pattern? → Validation error.
- What happens when attempting to edit or view an owner with a non-existent ID? → `IllegalArgumentException` indicating owner not found.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow the update of an existing owner's details (first name, last name, address, city, telephone).
- **FR-003**: System MUST allow owners to be searched by last name.
- **FR-004**: System MUST display a list of owners matching a search query.
- **FR-005**: System MUST allow navigation to an owner's detail page from the search results.
- **FR-006**: System MUST validate that owner's first name is not blank.
- **FR-007**: System MUST validate that owner's last name is not blank.
- **FR-008**: System MUST validate that owner's address is not blank.
- **FR-009**: System MUST validate that owner's city is not blank.
- **FR-010**: System MUST validate that owner's telephone number consists of exactly 10 digits.
- **FR-011**: System MUST handle cases where an owner ID does not exist during retrieval or update operations.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their personal details (address, city, telephone) and a collection of their pets.
- **Person**: Base entity for individuals, providing common fields like first name and last name. (Owner extends Person)

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created with valid data in under 1 minute.
- **SC-003**: 95% of owner creation/update attempts with invalid data result in clear, actionable error messages.
- **SC-004**: The system successfully handles requests for non-existent owner IDs without crashing, providing appropriate feedback.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse the existing `Person` entity for owner details.
- Data validation rules for owner fields (e.g., telephone format) are as specified in the provided context.
- The `OwnerRepository` and related persistence mechanisms are already in place and functional.
- The UI for displaying owner lists and detail pages will be developed separately but should accommodate the data structure defined here.