# Feature Specification: Pet Types Management

**Feature Branch**: `012-pet-types-spring-petclinic`

**Created**: 2026-08-29

**Status**: Draft

**Input**: User description: "pet types for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Add a new pet type (Priority: P1)

As a clinic administrator, I want to add a new type of pet (e.g., "Bird") to the system so that owners can select it when registering their pets.

**Why this priority**: This is a core functionality for managing the diversity of pets the clinic can handle.

**Independent Test**: Can be fully tested by navigating to the pet types management page, submitting a form with a unique pet type name, and verifying its appearance in the list.

**Acceptance Scenarios**:

1. **Given** I am on the pet types management page, **When** I submit a form to add a new pet type with the name "Bird", **Then** the new pet type "Bird" is successfully added and displayed in the list of pet types.

---

### User Story 2 - View existing pet types (Priority: P1)

As a clinic administrator, I want to view a list of all existing pet types so that I can see what options are currently available.

**Why this priority**: Essential for understanding the current state of pet type management and for users to make informed selections.

**Independent Test**: Can be fully tested by navigating to the pet types management page and verifying that all previously added pet types are displayed.

**Acceptance Scenarios**:

1. **Given** pet types like "Dog", "Cat", and "Rabbit" have been previously added, **When** I navigate to the pet types management page, **Then** all existing pet types ("Dog", "Cat", "Rabbit") are displayed.

---

### User Story 3 - Attempt to add a duplicate pet type (Priority: P2)

As a clinic administrator, when I try to add a pet type that already exists, I want to be informed that the name is a duplicate so that I don't accidentally create redundant entries.

**Why this priority**: Ensures data integrity and prevents confusion.

**Independent Test**: Can be fully tested by attempting to add a pet type with a name that is already present in the system and verifying the error message.

**Acceptance Scenarios**:

1. **Given** a pet type with the name "Dog" already exists, **When** I attempt to add another pet type named "Dog", **Then** an error message is displayed indicating that the pet type name already exists, and the duplicate "Dog" pet type is not added.

---

### User Story 4 - Associate a pet with a pet type (Priority: P1)

As a pet owner, I want to select a pet type when registering or updating my pet so that the system accurately records the kind of animal I own.

**Why this priority**: This is fundamental to the pet management functionality.

**Independent Test**: Can be tested by creating a new pet or editing an existing one, selecting a pet type from the available list, and verifying the selection is saved.

**Acceptance Scenarios**:

1. **Given** I am creating a new pet, **When** I select "Cat" from the pet type dropdown and provide other required pet details, **Then** the pet is successfully created and associated with the "Cat" type.
2. **Given** I am editing an existing pet currently of type "Dog", **When** I change the pet type to "Hamster" and save, **Then** the pet's type is updated to "Hamster".

---

### Edge Cases

- **Blank Pet Name**: Pet name is empty or contains only whitespace → system rejects with "required" validation error.
- **Null Pet Type**: Pet is new and its type is not set → system rejects with "required" validation error.
- **Null Birth Date**: Pet's birth date is not set → system rejects with "required" validation error.
- **Past Birth Date**: Pet's birth date is in the future → system rejects with "typeMismatch.birthDate" validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → system rejects with "duplicate" validation error.
- **Invalid Visit Date**: Visit date is not after the current date → system rejects with "typeMismatch.visitDate" validation error.
- **Non-existent Owner for Visit**: Attempting to add a visit for a pet belonging to a non-existent owner → system throws `IllegalArgumentException`.
- **Non-existent Pet for Visit**: Attempting to add a visit for a non-existent pet belonging to an owner → system throws `IllegalArgumentException`.
- **Duplicate Pet Name Across Different Owners**: Adding a pet with a name that already exists for a *different* owner → system allows the addition.
- **Exception Trigger**: Accessing the `/oups` endpoint → system throws a `RuntimeException` and returns an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST provide a list of all available pet types.
- **FR-002**: System MUST allow associating a pet with a specific pet type during pet creation and update.
- **FR-003**: System SHOULD ensure that pet type names are unique across all pet types.
- **FR-004**: System SHOULD validate that a pet type is selected during pet creation or update.
- **FR-005**: System SHOULD allow for the creation and management of different pet types.

### Key Entities *(include if feature involves data)*

- **PetType**: Represents a category of pet.
    - **name**: The name of the pet type (e.g., "Dog", "Cat", "Bird"). Must be unique and not blank.
- **Pet**: Represents an individual animal owned by a person.
    - **type**: A reference to the `PetType` this pet belongs to.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can add a new pet type in under 30 seconds.
- **SC-002**: The list of pet types displays correctly for all registered pet types.
- **SC-003**: 100% of new pets are successfully associated with a selected pet type.
- **SC-004**: Attempts to add duplicate pet type names are rejected with a clear error message.

## Assumptions

- Users interacting with pet type management are clinic administrators with appropriate permissions.
- The `NamedEntity` base class provides necessary ID and name fields.
- The underlying database can enforce uniqueness constraints on pet type names.
- The system will use standard web form validation for required fields.