# Feature Specification: Pet Types for Spring Petclinic

**Feature Branch**: `006-pet-types-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "pet types for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Add a new pet to an owner (Priority: P1)

Given an owner exists, When a new pet is created with valid details, Then the pet is added to the owner's list of pets and saved.

**Why this priority**: This is a core functionality for managing pets within the clinic. Without it, owners cannot register their animals.

**Independent Test**: Can be fully tested by creating an owner, then adding a pet to that owner, and verifying the pet appears in the owner's pet list and is persisted.

**Acceptance Scenarios**:

1. **Given** an existing owner, **When** a new pet is created with a name and a valid pet type, **Then** the pet is associated with the owner and saved.
2. **Given** an owner with no pets, **When** a new pet is created, **Then** the owner's pet list contains the newly added pet.

---

### User Story 2 - Update an existing pet's details (Priority: P2)

Given an existing pet belonging to an owner, When the pet's details are updated and saved, Then the pet's information is modified.

**Why this priority**: Allows for correction of errors or changes in a pet's information after initial registration.

**Independent Test**: Can be fully tested by creating a pet, then updating one of its attributes (e.g., name or type), and verifying the changes are reflected.

**Acceptance Scenarios**:

1. **Given** an existing pet, **When** its name is updated and saved, **Then** the pet's name is changed to the new value.
2. **Given** an existing pet, **When** its type is updated and saved, **Then** the pet's type is changed to the new value.

---

### User Story 3 - Prevent duplicate pet names for the same owner (Priority: P3)

Given an owner has a pet with a specific name, When an attempt is made to add another pet with the same name to that owner, Then a "duplicate" error is raised for the pet's name.

**Why this priority**: Prevents ambiguity and potential confusion when managing multiple pets for a single owner.

**Independent Test**: Can be fully tested by creating a pet for an owner, then attempting to add a second pet with the exact same name to the same owner, and verifying the duplicate name error.

**Acceptance Scenarios**:

1. **Given** an owner with a pet named "Buddy", **When** an attempt is made to add another pet named "Buddy" to the same owner, **Then** an error message indicating a duplicate name is displayed.

---

### Edge Cases

- What happens when a pet name is empty or contains only whitespace? → System rejects with "required" validation error.
- How does system handle a new pet where its type is not set? → System rejects with "required" validation error.
- How does system handle a pet's birth date not being set? → System rejects with "required" validation error.
- What happens when a pet's birth date is in the future? → System rejects with "typeMismatch.birthDate" validation error.
- What happens when attempting to add a pet with a name that already exists for the same owner? → System rejects with "duplicate" validation error for the pet's name.
- What happens when a visit date is not after the current date? → System rejects with "typeMismatch.visitDate" validation error.
- How does the system handle an invalid birth date format during an update? → System rejects with "typeMismatch" validation error for the "birthDate" field.
- What happens when attempting to access or modify resources for a non-existent owner ID? → System throws `IllegalArgumentException` indicating "Owner not found".
- What happens when attempting to access or modify a pet for a given owner ID where the pet ID does not exist? → System throws `IllegalArgumentException` indicating "Pet not found".
- What happens when attempting to add a pet with a name that already exists for a *different* owner? → System allows the operation, demonstrating case-insensitive duplicate name checking is per owner.
- What happens when accessing the "/oups" endpoint? → System throws a `RuntimeException` indicating an expected exception for showcasing error handling.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new pet types.
- **FR-002**: System MUST allow the retrieval of all available pet types.
- **FR-003**: System SHOULD allow the updating of existing pet types.
- **FR-004**: System SHOULD allow the deletion of existing pet types.
- **FR-005**: System MUST validate pet type names to ensure they are not empty.

### Key Entities *(include if feature involves data)*

- **PetType**: Represents different types of pets (e.g., Cat, Dog, Hamster). Attributes include a name.
- **Pet**: Represents an individual animal belonging to an owner. Attributes include name, birth date, and pet type.
- **Owner**: Represents the owner of one or more pets. Attributes include first name, last name, address, and phone number.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can add a new pet to an owner in under 1 minute.
- **SC-002**: System successfully retrieves all available pet types within 500ms.
- **SC-003**: 99% of attempts to add a pet with a duplicate name for the same owner result in a clear error message.
- **SC-004**: The system correctly validates pet type names, rejecting blank entries in 100% of cases.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse the existing `NamedEntity` structure for pet types.
- The system will use standard validation mechanisms for input fields.
- The system will handle errors gracefully with user-friendly messages.
- The scope of this feature is limited to managing pet types and their association with pets; advanced pet management features are out of scope.