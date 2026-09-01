# Feature Specification: Owner Management

**Feature Branch**: `006-owners-spring-petclinic`

**Created**: 2026-09-01

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to find owners by their last name so that I can quickly access their details and manage their pets.

**Why this priority**: This is a core functionality for managing customer information and is essential for daily operations.

**Independent Test**: Can be fully tested by searching for an existing owner's last name and verifying that their details are displayed, delivering immediate access to owner information.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists, **When** a user searches for owners with the last name "Franklin", **Then** the system redirects to the owner's details page.
2. **Given** multiple owners whose last names start with "Franklin" exist, **When** a user searches for owners with the last name "Franklin", **Then** the system displays a list of owners matching the partial last name.
3. **Given** multiple owners exist, **When** a user searches for owners with an empty last name or only whitespace, **Then** the system displays a list of all owners.

---

### User Story 2 - Add New Owner (Priority: P2)

As a clinic staff member, I want to add new owners to the system so that I can register new clients and their pets.

**Why this priority**: Expanding the client base is crucial for business growth.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying that the owner is successfully added to the system and appears in search results.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** the user fills in all required fields (first name, last name, address, city, telephone) with valid data and submits the form, **Then** a new owner is created and the user is redirected to the owner's details page.
2. **Given** the user is on the "Add Owner" page, **When** the user submits the form with a blank first name, **Then** an error message is displayed indicating the first name is required.
3. **Given** the user is on the "Add Owner" page, **When** the user submits the form with a telephone number that is not 10 digits, **Then** an error message is displayed indicating an invalid telephone format.

---

### User Story 3 - Update Owner Information (Priority: P2)

As a clinic staff member, I want to update an existing owner's information so that I can keep client records accurate.

**Why this priority**: Maintaining accurate client data is important for communication and service delivery.

**Independent Test**: Can be fully tested by selecting an owner, modifying their details, and verifying that the changes are saved and reflected on the owner's details page.

**Acceptance Scenarios**:

1. **Given** an existing owner is displayed on their details page, **When** the user clicks "Edit Owner", fills in updated information (e.g., changes city and telephone), and submits the form, **Then** the owner's information is updated and the details page reflects the changes.
2. **Given** an existing owner is displayed on their details page, **When** the user clicks "Edit Owner" and attempts to submit the form with a blank address, **Then** an error message is displayed indicating the address is required, and the owner's information is not updated.

---

### User Story 4 - Add New Pet for an Owner (Priority: P3)

As a clinic staff member, I want to add a new pet for an existing owner so that I can record their animal companions.

**Why this priority**: This is a supporting feature for owner management, enabling the full scope of pet clinic services.

**Independent Test**: Can be fully tested by navigating to an owner's details page, initiating the "Add Pet" process, filling in pet details, and verifying the pet is associated with the owner.

**Acceptance Scenarios**:

1. **Given** an owner's details page is displayed, **When** the user clicks "Add Pet", selects a pet type, enters a pet name, and provides a birth date, **Then** the new pet is successfully added and displayed under the owner's pets.
2. **Given** an owner's details page is displayed, **When** the user clicks "Add Pet" and attempts to submit the form with a blank pet name, **Then** an error message is displayed indicating the pet name is required.
3. **Given** an owner's details page is displayed, **When** the user clicks "Add Pet" and attempts to submit the form without selecting a pet type, **Then** an error message is displayed indicating the pet type is required.

---

### User Story 5 - Update Existing Pet Information (Priority: P3)

As a clinic staff member, I want to update an existing pet's information so that I can keep pet records accurate.

**Why this priority**: Similar to owner updates, maintaining accurate pet records is important.

**Independent Test**: Can be fully tested by selecting a pet, modifying its name or birth date, and verifying the changes are saved.

**Acceptance Scenarios**:

1. **Given** a pet is displayed on the owner's details page, **When** the user clicks "Edit Pet", changes the pet's name, and submits the form, **Then** the pet's name is updated.
2. **Given** a pet is displayed on the owner's details page, **When** the user clicks "Edit Pet", changes the pet's birth date, and submits the form, **Then** the pet's birth date is updated.

---

### Edge Cases

- What happens when an owner is created/updated with a blank address? → Validation error.
- What happens when an owner is created/updated with a blank city? → Validation error.
- What happens when an owner is created/updated with a telephone number not matching the 10-digit pattern? → Validation error.
- What happens when an owner is created/updated with a blank first name? → Validation error.
- What happens when an owner is created/updated with a blank last name? → Validation error.
- What happens when attempting to access or modify an owner with an ID that does not exist? → `IllegalArgumentException` indicating owner not found.
- What happens when a pet is created/updated with a blank name? → Validation error.
- What happens when a pet is created/updated without selecting a pet type? → Validation error.
- What happens when a pet is created/updated without providing a birth date? → Validation error.
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error.
- What happens when submitting a visit with a date in the past? → Validation error.
- What happens when attempting to add a visit for a pet that does not exist for a given owner? → `IllegalArgumentException` indicating pet not found.
- What happens when searching for owners with a last name that yields no results? → Validation error "notFound" on the lastName field.
- What happens when navigating to the `/oups` endpoint? → Throws a `RuntimeException` to showcase exception handling.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow updating an existing owner's information (address, city, telephone).
- **FR-003**: System MUST allow finding owners by last name, supporting exact and partial matches.
- **FR-004**: System MUST display a list of all owners when a search for owners with an empty last name is performed.
- **FR-005**: System MUST allow the creation of new pets for an owner.
- **FR-006**: System MUST allow updating an existing pet's name and birth date.
- **FR-007**: System SHOULD validate pet information during creation or update.
- **FR-008**: System SHOULD display a form for creating or updating pet details.
- **FR-009**: System SHOULD populate a list of available pet types when creating or updating a pet.
- **FR-010**: System MUST enforce that an owner's first name, last name, address, and city are not blank.
- **FR-011**: System MUST enforce that an owner's telephone number is exactly 10 digits.
- **FR-012**: System MUST enforce that a pet's name is not blank.
- **FR-013**: System MUST enforce that a pet's name is unique for a given owner.
- **FR-014**: System MUST enforce that a visit description is not blank.
- **FR-015**: System MUST handle non-existent owner IDs gracefully by throwing an `IllegalArgumentException`.
- **FR-016**: System MUST handle non-existent pet IDs for an owner gracefully by throwing an `IllegalArgumentException`.
- **FR-017**: System MUST display a "notFound" validation error on the lastName field when a search yields no results.
- **FR-018**: System MUST trigger a `RuntimeException` when navigating to the `/oups` endpoint for demonstration purposes.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Attributes include first name, last name, address, city, and telephone number. Has a one-to-many relationship with `Pet`.
- **Pet**: Represents a pet. Attributes include name, birth date, and type. Has a many-to-one relationship with `Owner` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the type of pet (e.g., Cat, Dog). Attributes include name.
- **Visit**: Represents a visit to the clinic. Attributes include date and description. Has a many-to-one relationship with `Pet`.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be added with all required fields in under 1 minute.
- **SC-003**: Existing owner information can be updated and saved in under 45 seconds.
- **SC-004**: New pets can be added to an owner's record in under 1 minute.
- **SC-005**: 99% of invalid input attempts (e.g., blank fields, incorrect phone format) result in clear validation errors presented to the user.
- **SC-006**: The system successfully handles requests for non-existent owner or pet IDs without crashing, providing appropriate error feedback.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- The existing `Person` and `NamedEntity` base classes will be utilized for common attributes.
- Data validation will be performed on the server-side.
- The `spring-petclinic` project's existing structure and dependencies will be maintained.
- The `ObjectRetrievalFailureException` will be used for cases where an entity is not found.
- The `/oups` endpoint is for testing exception handling and is not a user-facing feature.