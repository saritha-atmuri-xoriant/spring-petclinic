# Feature Specification: Owner Management

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-04

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing owners and is essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering a last name, and verifying the displayed results. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** a list of owners exists, **When** a user searches for owners by last name "Franklin", **Then** the system displays owners whose last name starts with "Franklin".
2. **Given** a list of owners exists, **When** a user searches for an owner last name that does not exist, **Then** the system displays a "No owners found" message.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a clinic staff member, I want to add new owners to the system so that I can register new clients and their pets.

**Why this priority**: Essential for onboarding new clients and expanding the customer base.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in valid details, and verifying the owner is created and their details page is displayed. Delivers the ability to add new clients.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields filled, **Then** the owner is created and redirected to the owner's details page.
2. **Given** a user is on the new owner form, **When** they submit the form with a blank first name, **Then** a validation error is displayed for the first name field.
3. **Given** a user is on the new owner form, **When** they submit the form with an invalid telephone number format, **Then** a validation error is displayed for the telephone field.

---

### User Story 3 - View Owner List (Priority: P2)

As a clinic staff member, I want to view a list of all owners so that I can get an overview of registered clients.

**Why this priority**: Provides a general overview and is useful for administrative tasks.

**Independent Test**: Can be fully tested by navigating to the owner list page and verifying that a paginated list of owners is displayed. Delivers visibility into the client base.

**Acceptance Scenarios**:

1. **Given** a user navigates to the owners list page, **When** the page loads, **Then** the system displays a paginated list of owners, showing at least their name and city.

---

### User Story 4 - Edit Owner Information (Priority: P2)

As a clinic staff member, I want to edit an existing owner's information so that I can keep their contact details up-to-date.

**Why this priority**: Ensures data accuracy and allows for updates to client information.

**Independent Test**: Can be fully tested by finding an owner, navigating to their edit page, making a change, saving it, and verifying the updated information. Delivers the ability to maintain accurate client records.

**Acceptance Scenarios**:

1. **Given** an owner exists, **When** a user navigates to the owner's edit page and updates their address, **Then** the owner's address is successfully updated and displayed on their details page.
2. **Given** an owner exists, **When** a user attempts to edit the owner's information with a blank city, **Then** a validation error is displayed for the city field, and the changes are not saved.

---

### User Story 5 - Add Pet to Owner (Priority: P3)

As a clinic staff member, I want to add a new pet to an existing owner's record so that I can track all their animals.

**Why this priority**: Important for comprehensive pet management within an owner's profile.

**Independent Test**: Can be fully tested by selecting an owner, navigating to their pet management section, adding a new pet with valid details, and verifying it appears in the owner's pet list. Delivers the ability to associate pets with owners.

**Acceptance Scenarios**:

1. **Given** an owner exists, **When** a user adds a new pet with a valid name and selects a pet type, **Then** the pet is successfully associated with the owner.
2. **Given** an owner exists, **When** a user attempts to add a pet with a blank name, **Then** a validation error is displayed for the pet's name.
3. **Given** an owner exists, **When** a user attempts to add a pet without selecting a pet type, **Then** a validation error is displayed for the pet type.

---

### Edge Cases

- What happens when an owner is created/updated with a blank first name? → Validation error.
- What happens when an owner is created/updated with a blank last name? → Validation error.
- What happens when an owner is created/updated with an invalid telephone number format? → Validation error.
- What happens when an owner is created/updated with a blank address? → Validation error.
- What happens when an owner is created/updated with a blank city? → Validation error.
- What happens when attempting to edit or view an owner with a non-existent ID? → `IllegalArgumentException` indicating owner not found.
- What happens when searching for owners with a last name that does not match any existing owners? → "notFound" validation error for the last name field.
- What happens when creating or updating a pet with a blank name? → Validation error "required".
- What happens when creating a pet without selecting a pet type? → Validation error "required".
- What happens when creating or updating a pet with a birth date in an incorrect format? → Validation error "typeMismatch".
- What happens when attempting to save a pet with a name that already exists for the same owner? → Validation error "duplicate".
- What happens when validating a pet object with a blank name? → `PetValidator` flags a field error for "name".
- What happens when validating a pet object with a null type? → `PetValidator` flags a field error for "type".
- What happens when validating a pet object with a null birth date? → `PetValidator` flags a field error for "birthDate".

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow searching for owners by last name.
- **FR-003**: System MUST allow viewing a list of all owners.
- **FR-004**: System MUST allow updating an existing owner's information (address, city, telephone).
- **FR-005**: System MUST validate owner information during creation and update, enforcing non-blank fields for first name, last name, address, city, and a 10-digit telephone number.
- **FR-006**: System MUST allow the creation of new pets for an owner.
- **FR-007**: System MUST allow updating an existing pet's name.
- **FR-008**: System SHOULD validate pet information during creation or update, enforcing non-blank pet names and selection of a pet type.
- **FR-009**: System SHOULD display a form for creating or updating pet details.
- **FR-010**: System SHOULD populate a list of available pet types for selection when creating or updating a pet.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual owner of pets. Attributes include first name, last name, address, city, and telephone number. Has a one-to-many relationship with `Pet`.
- **Pet**: Represents an animal owned by an owner. Attributes include name, birth date, and type. Has a many-to-one relationship with `Owner` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the species of a pet (e.g., Cat, Dog). Attributes include name. Has a one-to-many relationship with `Pet`.
- **Visit**: Represents a veterinary visit for a pet. Attributes include date and description. Has a many-to-one relationship with `Pet`.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 5 seconds.
- **SC-002**: New owners can be successfully created and their details viewed within 1 minute of form submission.
- **SC-003**: The owner list page loads within 3 seconds, displaying paginated results.
- **SC-004**: 95% of owner information updates are successfully saved and reflected immediately.
- **SC-005**: New pets can be added to an owner's record with a 100% success rate for valid inputs.

## Assumptions

- Users performing these actions are clinic staff with appropriate permissions.
- The system has access to a predefined list of pet types.
- Data validation messages are user-friendly and informative.
- The system will handle concurrent updates to owner data gracefully.
- The `spring-petclinic` application is already set up with basic data for owners and pet types.