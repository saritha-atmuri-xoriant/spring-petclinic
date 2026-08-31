# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `063-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for managing pet owners and is essential for basic application usability.

**Independent Test**: Can be fully tested by searching for an existing owner's last name and verifying the correct owner details page is displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the "Find Owners" page, **When** they enter "Franklin" in the "Last Name" field and click "Search", **Then** the system displays the details for the owner named Franklin.
2. **Given** a user is on the "Find Owners" page, **When** they enter a last name that does not exist and click "Search", **Then** the system displays a "No owners found" message.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and the user is redirected to the owner's list.

**Why this priority**: The ability to add new owners is fundamental to the application's purpose.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner appears in the owner list.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Add Owner", **Then** the new owner is saved and the user is redirected to the "Owner List" page, displaying the newly added owner.

---

### User Story 3 - Update an Existing Owner (Priority: P2)

Given an owner exists, When a user edits and saves the owner's details with valid information, Then the owner's information is updated.

**Why this priority**: Allows for correction of errors or changes in owner information.

**Independent Test**: Can be fully tested by editing an existing owner's details and verifying the changes are reflected on their detail page and the owner list.

**Acceptance Scenarios**:

1. **Given** a user is viewing an owner's details, **When** they click "Edit Owner", **Then** the owner's details are pre-populated in an editable form.
2. **Given** the owner's details are pre-populated in the edit form, **When** the user modifies the telephone number and clicks "Update Owner", **Then** the owner's telephone number is updated, and the user is redirected to the owner's details page showing the new number.

---

### User Story 4 - Add a New Pet for an Owner (Priority: P2)

Given an owner exists, When a user adds a new pet for that owner, Then the pet is associated with the owner.

**Why this priority**: Core functionality for managing a pet owner's pets.

**Independent Test**: Can be fully tested by selecting an owner, adding a new pet with valid details, and verifying the pet appears under the owner's profile.

**Acceptance Scenarios**:

1. **Given** a user is viewing an owner's details, **When** they click "Add New Pet", **Then** a form to add a new pet is displayed, pre-populated with the owner's information.
2. **Given** the new pet form is displayed, **When** the user enters a valid pet name, selects a pet type, and provides a birth date, and clicks "Add Pet", **Then** the new pet is created and associated with the owner, appearing in the owner's pet list.

---

### User Story 5 - Add a New Visit for a Pet (Priority: P3)

Given a pet exists for an owner, When a user adds a new visit for that pet, Then the visit is recorded for the pet.

**Why this priority**: Essential for tracking pet health history.

**Independent Test**: Can be fully tested by selecting a pet, adding a new visit with valid details, and verifying the visit appears in the pet's visit history.

**Acceptance Scenarios**:

1. **Given** a user is viewing a pet's details, **When** they click "Add New Visit", **Then** a form to add a new visit is displayed, pre-populated with the pet's information.
2. **Given** the new visit form is displayed, **When** the user enters a valid visit date and description and clicks "Add Visit", **Then** the new visit is recorded and appears in the pet's visit history.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error displayed on the form.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error displayed on the form.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error displayed on the form.
- **Blank Address**: Owner creation/update with a blank address → validation error displayed on the form.
- **Blank City**: Owner creation/update with a blank city → validation error displayed on the form.
- **Non-existent Owner for Edit**: Attempting to edit an owner with an ID that does not exist → `IllegalArgumentException` is thrown and handled gracefully by displaying an error message to the user.
- **Non-existent Owner for Pet Creation**: Attempting to create a pet for an owner with an ID that does not exist → `IllegalArgumentException` is thrown and handled gracefully by displaying an error message to the user.
- **Non-existent Owner for Visit Creation**: Attempting to create a visit for an owner with an ID that does not exist → `IllegalArgumentException` is thrown and handled gracefully by displaying an error message to the user.
- **Non-existent Pet for Visit Creation**: Attempting to create a visit for a pet with an ID that does not exist for a given owner → `IllegalArgumentException` is thrown and handled gracefully by displaying an error message to the user.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error displayed on the form.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error displayed on the form.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → validation error displayed on the form.
- **Duplicate Pet Name for Same Owner**: Attempting to save a pet with a name that already exists for the same owner → validation error displayed on the form.
- **Invalid Visit Date**: Visit creation with a date that is not in the future → validation error displayed on the form.
- **Duplicate Pet Name in Concurrency**: Concurrent attempts to create pets with the same name for the same owner → only one successful creation, others fail with a clear error message indicating the pet name is already in use.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow finding owners by their last name.
- **FR-005**: System SHOULD allow adding a new visit for a pet.
- **FR-006**: System MUST allow the creation of new owners.
- **FR-007**: System MUST allow the update of existing owner details.
- **FR-008**: System MUST validate owner information during creation and update.
- **FR-009**: System MUST allow viewing an owner's details, including their pets and visits.
- **FR-010**: System MUST allow viewing a pet's details, including its visits.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include first name, last name, address, city, and telephone number. Has a relationship with multiple Pets.
- **Pet**: Represents a pet. Key attributes include name, birth date, and type. Has relationships with an Owner and multiple Visits.
- **PetType**: Represents the type of a pet (e.g., cat, dog). Key attribute is its name.
- **Visit**: Represents a visit to the clinic for a pet. Key attributes include date and description. Has a relationship with a Pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created and displayed in the owner list within 5 seconds of form submission.
- **SC-003**: Owner and pet information can be updated and reflected on detail pages within 3 seconds.
- **SC-004**: 95% of users can successfully add a new pet or visit without encountering validation errors on the first attempt, assuming valid input.
- **SC-005**: The system supports up to 500 concurrent users browsing owner information without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- Standard date and time formats will be used for user input.
- The underlying database is capable of storing and retrieving the required owner and pet data.
- The application will be deployed in an environment where it can communicate with its database.