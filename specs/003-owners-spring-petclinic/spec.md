# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `003-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for managing pet clinic data, allowing staff to quickly access specific owner information.

**Independent Test**: Can be fully tested by searching for an existing owner's last name and verifying the redirect to their detail page.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists in the system, **When** a user navigates to the "Find Owners" page and enters "Franklin" in the last name field, **Then** the system displays the details page for the owner named "Franklin".

---

### User Story 2 - Find Owners with Partial Last Name Match (Priority: P2)

Given multiple owners exist whose last names start with "Smith", When a user searches for owners with the last name "Smith", Then a list of all matching owners is displayed.

**Why this priority**: This allows for efficient searching when the exact last name is not known or for handling common last names.

**Independent Test**: Can be fully tested by searching for a partial last name that matches multiple owners and verifying that a list of all matching owners is displayed.

**Acceptance Scenarios**:

1. **Given** multiple owners exist with last names starting with "Smith" (e.g., "Smith", "Smithson"), **When** a user navigates to the "Find Owners" page and enters "Smith" in the last name field, **Then** a list displaying all owners whose last name starts with "Smith" is shown.

---

### User Story 3 - Handle Empty Last Name Search (Priority: P3)

Given multiple owners exist, When a user searches for owners with an empty or whitespace-only last name, Then all owners are displayed in a list.

**Why this priority**: This provides a way to view all registered owners, useful for administrative tasks or general overview.

**Independent Test**: Can be fully tested by submitting an empty search query on the "Find Owners" page and verifying that all owners are listed.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** a user navigates to the "Find Owners" page and leaves the last name field empty or enters only whitespace, **Then** a list of all owners in the system is displayed.

---

### Edge Cases

- What happens when an owner is created or updated with a blank first name? → Validation error.
- What happens when an owner is created or updated with a blank last name? → Validation error.
- What happens when an owner is created or updated with a telephone number not matching the `\d{10}` pattern? → Validation error.
- What happens when an owner is created or updated with a blank address? → Validation error.
- What happens when an owner is created or updated with a blank city? → Validation error.
- What happens when attempting to edit an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when searching for owners by last name when no owners match? → Validation error "notFound" for lastName.
- What happens when a pet is created or updated with a blank name? → Validation error "required".
- What happens when a pet is created or updated without selecting a pet type? → Validation error "required".
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error "duplicate".
- What happens when a pet is created or updated with a birth date in an incorrect format (e.g., "2015/02/12")? → Validation error "typeMismatch".
- What happens when a pet is created or updated with a null birth date? → Validation error.
- What happens when booking a visit with a date that is not in the future? → Validation error "typeMismatch.visitDate".
- What happens when attempting to book a visit for a pet that does not exist for a given owner? → `IllegalArgumentException` is thrown.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new pets for an owner.
- **FR-002**: System MUST allow the updating of existing pet information.
- **FR-003**: System SHOULD validate pet data upon creation or update.
- **FR-004**: System SHOULD allow owners to be searched by last name.
- **FR-005**: System SHOULD display a list of pets associated with an owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual who owns one or more pets. Includes fields for first name, last name, address, city, and telephone number. Has a one-to-many relationship with `Pet`.
- **Pet**: Represents an animal owned by an `Owner`. Includes fields for name, birth date, and type. Has a many-to-one relationship with `Owner` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the category of a pet (e.g., Dog, Cat, Hamster). Includes a name field.
- **Visit**: Represents a veterinary visit for a `Pet`. Includes fields for date and description. Has a many-to-one relationship with `Pet`.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find an owner by last name in under 3 seconds.
- **SC-002**: The system displays a list of matching owners for partial last name searches within 3 seconds.
- **SC-003**: All owners are displayed when searching with an empty last name within 5 seconds.
- **SC-004**: 95% of pet creation/update operations complete successfully with valid data.
- **SC-005**: Validation errors are clearly presented to the user for invalid data inputs.

## Assumptions

- Users have stable internet connectivity.
- The system will be used by veterinary clinic staff.
- Data validation rules are enforced at the application level.
- The primary language for the application is English.
- The system will reuse existing `Person` and `NamedEntity` base classes for common attributes.
- The telephone number format `\d{10}` is the standard for all owners.
- Pet birth dates are stored in `yyyy-MM-dd` format.
- Visit dates are stored in `yyyy-MM-dd` format.