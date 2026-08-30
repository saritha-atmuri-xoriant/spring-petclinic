# Feature Specification: Pet Types for Spring Petclinic

**Feature Branch**: `035-pet-types-spring-petclinic`

**Created**: 2026-08-30

**Status**: Draft

**Input**: User description: "pet types for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Add a new pet with a type (Priority: P1)

**Description**: As a clinic staff member, I want to add a new pet to an owner's record, ensuring I can select its type from a predefined list, so that the pet's information is accurately categorized.

**Why this priority**: This is a core functionality for managing pets within the clinic.

**Independent Test**: Can be fully tested by creating a new pet for an existing owner and selecting a pet type from the available list, verifying the pet is saved with the correct type.

**Acceptance Scenarios**:

1.  **Given** an existing owner, **When** I navigate to add a new pet for this owner, **And** I select "Dog" from the pet type dropdown, **And** I fill in the pet's name and birth date, **Then** the new pet is successfully added to the owner's record with the "Dog" type.
2.  **Given** an existing owner, **When** I navigate to add a new pet for this owner, **And** I leave the pet type selection blank, **Then** the system displays a validation error indicating that the pet type is required.

---

### User Story 2 - View available pet types (Priority: P2)

**Description**: As a clinic staff member, I want to see a list of all available pet types when adding or editing a pet, so that I can correctly categorize the animal.

**Why this priority**: Essential for supporting the primary pet management workflow.

**Independent Test**: Can be tested by navigating to the "Add Pet" or "Edit Pet" forms and verifying that all predefined pet types are present in the selection dropdown.

**Acceptance Scenarios**:

1.  **Given** I am on the "Add Pet" form, **When** I look at the pet type selection, **Then** I see a list including "Cat", "Dog", "Lizard", and "Parrot".
2.  **Given** I am on the "Edit Pet" form for an existing pet, **When** I look at the pet type selection, **Then** I see a list including "Cat", "Dog", "Lizard", and "Parrot".

---

### User Story 3 - Update an existing pet's type (Priority: P3)

**Description**: As a clinic staff member, I want to update the pet type of an existing pet if it was entered incorrectly, so that the pet's record remains accurate.

**Why this priority**: Supports data accuracy and correction of errors.

**Independent Test**: Can be tested by editing an existing pet, changing its type, and verifying the change is saved.

**Acceptance Scenarios**:

1.  **Given** a pet named "Buddy" is currently of type "Dog", **When** I edit Buddy's details and change the pet type to "Cat", **And** I save the changes, **Then** Buddy's record is updated to show the pet type as "Cat".

---

### Edge Cases

- What happens when a pet type name is blank or exceeds 30 characters? → System rejects with validation error "required" or "size" respectively.
- What happens when a pet is created without selecting a pet type? → System rejects with validation error "required" for pet type.
- What happens when a pet is created with a null birth date? → System rejects with validation error "required" for birth date.
- What happens when a pet's birth date is entered in the future? → System rejects with "typeMismatch.birthDate" validation error.
- What happens when attempting to add a pet with a name that already exists for the same owner? → System rejects with "duplicate" validation error.
- What happens when attempting to add a pet with a name that exists for a different owner? → System allows the operation, demonstrating case-insensitive duplicate name handling is per owner.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST provide a collection of available pet types (e.g., Cat, Dog, Lizard, Parrot).
- **FR-002**: System MUST allow associating a pet with a pet type during pet creation.
- **FR-003**: System MUST allow changing the pet type of an existing pet.
- **FR-004**: System SHOULD ensure that a pet type is selected when creating a new pet.
- **FR-005**: System SHOULD validate that the pet type is not null for new pets.
- **FR-006**: System MUST retrieve all pet types for populating forms used for pet creation and editing.
- **FR-007**: System MUST enforce that pet type names are not blank.
- **FR-008**: System MUST enforce that pet type names do not exceed 30 characters.

### Key Entities *(include if feature involves data)*

- **PetType**: Represents a classification of a pet (e.g., "Cat", "Dog"). It has a name and is associated with pets.
- **Pet**: Represents an individual animal owned by an owner. It has a name, birth date, and is associated with a `PetType`.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: 100% of new pets are created with a valid, selected pet type.
- **SC-002**: Users can successfully update the pet type for 100% of existing pets.
- **SC-003**: The list of available pet types displayed in forms is accurate and complete.
- **SC-004**: Validation errors for blank or oversized pet type names are correctly triggered in 100% of cases.

## Assumptions

- Users have stable internet connectivity.
- The list of initial pet types will be "Cat", "Dog", "Lizard", and "Parrot".
- The system will reuse the existing `NamedEntity` abstract class for `PetType`.
- The `Pet` entity will correctly reference the `PetType` entity via a ManyToOne relationship.
- Validation for pet type names (blank, size) will be implemented as per standard Spring validation annotations.