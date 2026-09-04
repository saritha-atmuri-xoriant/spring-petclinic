# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-04

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - View Owner List (Priority: P1)

Users should be able to see a list of all owners currently registered in the system. This list should display key information for each owner.

**Why this priority**: This is a fundamental feature for managing and viewing pet owners, essential for most operations within the pet clinic.

**Independent Test**: Can be fully tested by navigating to the owner list page and verifying that all existing owners are displayed with their basic details.

**Acceptance Scenarios**:

1. **Given** there are multiple owners registered in the system, **When** a user navigates to the "Owners" page, **Then** a list of all owners is displayed, showing their first name, last name, address, city, and telephone number.
2. **Given** there are no owners registered in the system, **When** a user navigates to the "Owners" page, **Then** a message indicating "No owners found" is displayed.

---

### User Story 2 - Find Owners by Last Name (Priority: P1)

Users should be able to search for owners by providing a prefix of their last name. The system should then display a list of all owners whose last names match the provided prefix.

**Why this priority**: This is a critical feature for quickly locating specific owners, improving efficiency for clinic staff.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying that only owners matching that prefix are returned.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** a user searches for owners with the last name prefix "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** there are owners with last names "Davis" and "Miller", **When** a user searches for owners with the last name prefix "Xy", **Then** a message indicating "No owners found" is displayed.
3. **Given** there are owners with last names "Johnson" and "Jonsson", **When** a user searches for owners with the last name prefix "John", **Then** a list containing "Johnson" is displayed.

---

### User Story 3 - Create a New Owner (Priority: P2)

Users should be able to add new owners to the system by filling out a form with the owner's details. Upon successful submission, the new owner should be created and the user should be redirected to the owner's detail page.

**Why this priority**: Essential for onboarding new clients and expanding the pet clinic's database.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying that the owner is created and their details page is displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the "New Owner" form, **When** they enter valid details for first name, last name, address, city, and telephone, and submit the form, **Then** the owner is successfully created and the user is redirected to the newly created owner's detail page.
2. **Given** a user is on the "New Owner" form, **When** they attempt to submit the form with a blank last name, **Then** a validation error message is displayed next to the last name field, and the owner is not created.
3. **Given** a user is on the "New Owner" form, **When** they attempt to submit the form with a telephone number that is not 10 digits, **Then** a validation error message is displayed next to the telephone field, and the owner is not created.

---

### User Story 4 - View Owner Details (Priority: P2)

Users should be able to view the detailed information of a specific owner, including their personal details and a list of their associated pets.

**Why this priority**: Allows users to access comprehensive information about a specific owner and their pets.

**Independent Test**: Can be fully tested by selecting an owner from the list and verifying that all their details and pets are displayed correctly.

**Acceptance Scenarios**:

1. **Given** an owner with associated pets exists, **When** a user clicks on the owner's name from the owner list, **Then** the owner's detail page is displayed, showing their first name, last name, address, city, telephone, and a list of their pets with their names and types.
2. **Given** an owner with no pets exists, **When** a user clicks on the owner's name from the owner list, **Then** the owner's detail page is displayed, showing their personal details and a message indicating "No pets found".

---

### User Story 5 - Edit Owner Information (Priority: P3)

Users should be able to edit the details of an existing owner. This includes updating their address, city, and telephone number.

**Why this priority**: Allows for correction of errors or updating of owner information as it changes.

**Independent Test**: Can be fully tested by navigating to an owner's detail page, initiating the edit process, changing a field, saving, and verifying the update.

**Acceptance Scenarios**:

1. **Given** a user is viewing an owner's detail page, **When** they click the "Edit Owner" button, **Then** the owner's details are displayed in an editable form.
2. **Given** a user is on the "Edit Owner" form, **When** they update the address and save the changes, **Then** the owner's detail page is refreshed, showing the updated address.
3. **Given** a user is on the "Edit Owner" form, **When** they attempt to save with a blank city, **Then** a validation error message is displayed next to the city field, and the changes are not saved.

---

### Edge Cases

- What happens when an owner is edited with a blank first name? → Validation error.
- What happens when an owner is edited with a blank last name? → Validation error.
- What happens when an owner is edited with an invalid telephone format? → Validation error.
- What happens when an owner is edited with a blank address? → Validation error.
- What happens when an owner is edited with a blank city? → Validation error.
- What happens when attempting to edit an owner that does not exist? → `IllegalArgumentException` is thrown.
- What happens when attempting to create a pet for an owner that does not exist? → `IllegalArgumentException` is thrown.
- What happens when attempting to create a visit for a pet belonging to an owner that does not exist? → `IllegalArgumentException` is thrown.
- What happens when attempting to create a visit for a pet that does not exist for a given owner? → `IllegalArgumentException` is thrown.
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error.
- What happens when searching for owners by last name when no owners match the criteria? → `notFound` validation error is added to the `lastName` field.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow updating an existing owner's details (address, city, telephone).
- **FR-003**: System MUST allow searching for owners by last name prefix.
- **FR-004**: System MUST display a list of all owners.
- **FR-005**: System MUST display the details of a specific owner, including their associated pets.
- **FR-006**: System MUST allow the creation of new pets for an owner.
- **FR-007**: System MUST allow updating an existing pet's details.
- **FR-008**: System SHOULD validate owner information (first name, last name, address, city, telephone) before saving.
- **FR-009**: System SHOULD validate pet information (name, birth date, type) before saving.
- **FR-010**: System SHOULD validate visit information (date, description) before saving.
- **FR-011**: System MUST prevent the binding of `id` fields when creating or updating owners.
- **FR-012**: System MUST prevent the binding of `id` fields when creating or updating visits.
- **FR-013**: System MUST prevent duplicate pet names for the same owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Includes first name, last name, address, city, telephone, and a collection of associated pets.
- **Pet**: Represents a pet belonging to an owner. Includes name, birth date, type, and a collection of visits.
- **PetType**: Represents the type of a pet (e.g., cat, dog).
- **Visit**: Represents a vet visit for a pet. Includes date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 2 seconds.
- **SC-002**: New owners can be created and their details page viewed within 3 minutes of form submission.
- **SC-003**: The owner list page loads completely within 3 seconds for up to 100 owners.
- **SC-004**: 95% of users can successfully create or edit an owner without encountering validation errors on the first attempt.
- **SC-005**: The system correctly displays all associated pets for an owner.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing `Person` and `NamedEntity` base classes for owner and pet attributes.
- Data validation rules (e.g., telephone format, non-blank fields) are enforced at the application layer.
- The system will use standard JPA for persistence.
- The user interface will provide clear feedback for validation errors.
- The system will handle non-existent owner/pet lookups gracefully by returning appropriate error messages or exceptions.
- The `id` fields for owners and pets are auto-generated by the persistence layer and should not be provided by the user during creation or update.