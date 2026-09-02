# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-08-29

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's detail page.

**Why this priority**: This is a core functionality for managing pet owners and is a primary user interaction.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and submitting. The system should then display the details of the owner named Franklin.

**Acceptance Scenarios**:

1. **Given** an owner named "John Franklin" exists in the system, **When** a user searches for owners with the last name "Franklin", **Then** the system displays the detail page for "John Franklin".

---

### User Story 2 - Find Owners with Partial Last Name Match (Priority: P2)

Given multiple owners whose last names start with "Franklin" exist, When a user searches for owners with the last name "Franklin", Then the system displays a list of owners on the ownersList view.

**Why this priority**: Allows for flexible searching and discovery of owners when the exact last name is not known.

**Independent Test**: Can be fully tested by searching for a partial last name that matches multiple owners. The system should then display a list of all matching owners.

**Acceptance Scenarios**:

1. **Given** owners "John Franklin" and "Jane Franklin" exist, **When** a user searches for owners with the last name "Franklin", **Then** the system displays a list containing both "John Franklin" and "Jane Franklin".

---

### User Story 3 - Handle Empty or Whitespace-Only Last Name Search (Priority: P3)

Given multiple owners exist, When a user searches for owners with a last name consisting only of whitespace, Then the system displays all owners on the ownersList view.

**Why this priority**: Ensures graceful handling of user input and provides a way to view all owners if no specific search criteria are provided.

**Independent Test**: Can be fully tested by entering only spaces into the last name search field and submitting. The system should then display all registered owners.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** a user searches for owners with a last name consisting only of spaces, **Then** the system displays a list of all registered owners.

---

### Edge Cases

- What happens when an owner's first name is blank? → Validation error.
- What happens when an owner's address is blank? → Validation error.
- What happens when an owner's telephone number does not match the `\d{10}` pattern? → Validation error.
- What happens when searching for an owner last name that yields no results? → An "owner not found" message is displayed.
- What happens when creating a pet with a blank name? → Validation error "required".
- What happens when creating a pet without specifying a type? → Validation error "required".
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error "duplicate".

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST display a form to create or update a pet, pre-populated with owner details.
- **FR-003**: System SHOULD validate pet information before saving.
- **FR-004**: System SHOULD allow finding owners by their last name.
- **FR-005**: System SHOULD allow updating a pet's name.
- **FR-006**: System MUST allow creating new owners.
- **FR-007**: System MUST allow updating existing owner details (address, city, telephone).
- **FR-008**: System MUST allow deleting owners.
- **FR-009**: System MUST allow creating new pet types.
- **FR-010**: System MUST allow updating existing pet types.
- **FR-011**: System MUST allow deleting pet types.
- **FR-012**: System MUST allow creating new visits for a pet.
- **FR-013**: System MUST allow updating existing visit details.
- **FR-014**: System MUST allow deleting visits.
- **FR-015**: System MUST enforce that owner's first name, last name, address, city, and telephone are not blank.
- **FR-016**: System MUST enforce that pet's name is not blank.
- **FR-017**: System MUST enforce that pet's telephone is exactly 10 digits.
- **FR-018**: System MUST enforce that a pet's name is unique for a given owner.
- **FR-019**: System MUST disallow setting owner's address and telephone fields directly when creating or updating an owner.
- **FR-020**: System MUST disallow setting the ID field directly when creating or updating a visit.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual owner of pets. Attributes include first name, last name, address, city, and telephone number. Has a one-to-many relationship with `Pet`.
- **Pet**: Represents an individual pet. Attributes include birth date and type. Has a many-to-one relationship with `PetType` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog). Attributes include name.
- **Visit**: Represents a visit to the veterinarian for a pet. Attributes include date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully find owners by last name in under 3 seconds.
- **SC-002**: The system can support the creation and management of up to 1000 owners and their associated pets without performance degradation.
- **SC-003**: 95% of users can successfully add a new pet to an existing owner on their first attempt.
- **SC-004**: Validation errors for owner and pet data are displayed clearly and immediately upon form submission.
- **SC-005**: The system correctly handles searches for partial last names, returning all relevant owners.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms will be leveraged if applicable to owner management.
- The data for owners, pets, pet types, and visits will be persisted in a relational database.
- The primary language for user interaction will be English.