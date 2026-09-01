# Feature Specification: Owner Management

**Feature Branch**: `023-owners-spring-petclinic`

**Created**: 2026-09-01

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for navigating the pet clinic system and finding existing owner information.

**Independent Test**: Can be fully tested by entering "Franklin" in the owner search field and verifying redirection to the correct owner's details page.

**Acceptance Scenarios**:

1. **Given** the system has an owner with the last name "Franklin" and first name "George", **When** a user searches for owners with the last name "Franklin", **Then** the system displays the owner's details page for George Franklin.
2. **Given** no owners exist with the last name "Smith", **When** a user searches for owners with the last name "Smith", **Then** the system displays a "Owner not found" message.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and the user is redirected to the owner's list.

**Why this priority**: Essential for onboarding new clients and their pets into the system.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying redirection to the owner list with the new owner present.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields filled (first name, last name, address, city, telephone), **Then** the new owner is successfully created and the user is redirected to the owner list page.

---

### User Story 3 - Update an Existing Owner (Priority: P2)

Given an existing owner's details are displayed, When a user modifies and submits the owner's information, Then the owner's details are updated and the updated details are reflected.

**Why this priority**: Allows for maintaining accurate owner information as it changes.

**Independent Test**: Can be fully tested by selecting an owner, modifying a field (e.g., telephone number), saving, and verifying the change.

**Acceptance Scenarios**:

1. **Given** an owner's details are displayed, **When** a user changes the owner's telephone number and submits the form, **Then** the owner's telephone number is updated in the system.

---

### User Story 4 - Add a New Pet to an Owner (Priority: P2)

Given an owner's details are displayed, When a user adds a new pet for that owner, Then the new pet is associated with the owner and appears in their pet list.

**Why this priority**: Core functionality for managing a pet owner's pets.

**Independent Test**: Can be fully tested by navigating to an owner's details, adding a new pet with valid information, and verifying its appearance in the owner's pet list.

**Acceptance Scenarios**:

1. **Given** an owner's details are displayed, **When** a user adds a new pet with a valid name and birth date, **Then** the new pet is successfully added to the owner's record.

---

### User Story 5 - Add a Visit for a Pet (Priority: P3)

Given a pet's details are displayed, When a user adds a new visit for that pet, Then the new visit is recorded and associated with the pet.

**Why this priority**: Tracks veterinary appointments and history for pets.

**Independent Test**: Can be fully tested by navigating to a pet's details, adding a new visit with a valid date and description, and verifying its presence.

**Acceptance Scenarios**:

1. **Given** a pet's details are displayed, **When** a user adds a new visit with a valid date and description, **Then** the visit is successfully recorded for the pet.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Owner Not Found During Find**: Searching for an owner by last name results in no matches → validation error "notFound" is added to the "lastName" field.
- **Blank Pet Name**: Creating or updating a pet with a blank name → validation error "required" is added to the "name" field.
- **Missing Pet Type**: Creating or updating a pet without selecting a type → validation error "required" is added to the "type" field.
- **Invalid Pet Birth Date Format**: Creating or updating a pet with a birth date in an incorrect format (e.g., "2015/02/12") → validation error "typeMismatch" is added to the "birthDate" field.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error "duplicate" is added to the "name" field.
- **Invalid Visit Date**: Booking a visit with a date that is not in the future → validation error "typeMismatch.visitDate" is added to the "date" field.
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet that does not exist for a given owner → `IllegalArgumentException` is thrown.
- **Unsynchronized Translation Files**: If translation files (e.g., `messages_es.properties`) are missing keys present in the base file (`messages.properties`) → a test failure is reported indicating missing keys.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow searching for owners by last name.
- **FR-005**: System SHOULD allow adding new visits for a pet.
- **FR-006**: System MUST allow the creation of a new owner.
- **FR-007**: System MUST allow the update of an existing owner's details.
- **FR-008**: System MUST validate owner information during creation or update, including address, city, and telephone format.
- **FR-009**: System MUST ensure pet names are unique for a given owner.
- **FR-010**: System MUST validate visit information during creation, including date.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (name, address, city, telephone) and a collection of associated pets.
- **Pet**: Represents a pet, including its name, birth date, type, and a history of visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a veterinary visit for a pet, including the date and a description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 2 seconds.
- **SC-002**: New owners can be created with valid information in under 1 minute.
- **SC-003**: Pet and visit information can be added to an owner's record without significant delay.
- **SC-004**: 99% of owner and pet data entries pass validation checks.
- **SC-005**: System supports up to 500 concurrent users managing owner and pet data.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing authentication mechanisms if applicable (though not explicitly detailed in the provided context).
- Data persistence is handled by an underlying repository layer, as implied by the context.
- Translation files for internationalization are managed separately and are assumed to be synchronized.
- The `Person` class is a base for `Owner` and contains first and last name fields.
- `NamedEntity` is a base for `Pet` and `PetType` and contains a `name` field.
- `BaseEntity` is a base for `Visit` and contains an `id` field.
- The `telephone` field is expected to be a string of exactly 10 digits.
- Pet birth dates and visit dates are expected in "yyyy-MM-dd" format.
- The system will provide user-friendly error messages for validation failures.