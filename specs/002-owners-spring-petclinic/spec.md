# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-03

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for accessing owner information and is critical for basic system usability.

**Independent Test**: Can be fully tested by entering "Franklin" in the last name search field and verifying navigation to the correct owner's detail page.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists in the system, **When** a user navigates to the owner search page and enters "Franklin" in the last name field, **Then** the system redirects to the details page for the owner "Franklin".

---

### User Story 2 - Find Owners with a Partial Last Name (Priority: P2)

Given multiple owners whose last names start with "Smith" exist, When a user searches for owners with the last name "Smith", Then a list of all matching owners is displayed.

**Why this priority**: This allows for more flexible searching and is important for users who may not know the exact spelling of a last name.

**Independent Test**: Can be fully tested by entering "Smith" in the last name search field and verifying that all owners with last names starting with "Smith" are displayed.

**Acceptance Scenarios**:

1. **Given** multiple owners exist with last names starting with "Smith" (e.g., "Smith", "Smyth"), **When** a user navigates to the owner search page and enters "Smith" in the last name field, **Then** a list displaying all owners whose last name starts with "Smith" is shown.

---

### User Story 3 - Handle Empty Last Name Search (Priority: P3)

Given there are multiple owners in the system, When a user searches for owners with an empty or whitespace-only last name, Then all owners are displayed in a list.

**Why this priority**: This provides a way to view all registered owners, which can be useful for administrative purposes or general browsing.

**Independent Test**: Can be fully tested by leaving the last name search field empty and verifying that all owners in the system are displayed.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** a user navigates to the owner search page and leaves the last name field empty or enters only whitespace, **Then** a list of all owners in the system is displayed.

---

### Edge Cases

- What happens when an owner is created or updated with a blank first name? **Validation error.**
- What happens when an owner is created or updated with a blank last name? **Validation error.**
- What happens when an owner is created or updated with a telephone number that does not match the `\d{10}` pattern? **Validation error.**
- What happens when an owner is created or updated with a blank address? **Validation error.**
- What happens when an owner is created or updated with a blank city? **Validation error.**
- What happens when attempting to edit or view an owner with an ID that does not exist? **`IllegalArgumentException` thrown.**
- What happens when searching for owners with a last name that yields no results? **`notFound` validation error on `lastName` field.**
- What happens when creating or updating a pet with a blank name? **`required` validation error on the `name` field.**
- What happens when creating a pet without selecting a pet type? **`required` validation error on the `type` field.**
- What happens when creating or updating a pet with a birth date in an incorrect format (e.g., "2015/02/12")? **`typeMismatch` validation error on the `birthDate` field.**
- What happens when attempting to add a pet with a name that already exists for the same owner? **`duplicate` validation error on the `name` field.**
- What happens when creating a visit with a blank date? **Validation error.**
- What happens when creating a visit with a date that is not after the current date? **`typeMismatch.visitDate` validation error on the `date` field.**
- What happens when attempting to add a visit for a pet ID that does not exist for the specified owner? **`IllegalArgumentException` thrown.**
- What happens when accessing the `/oups` endpoint? **`RuntimeException` is thrown, indicating an expected error scenario.**

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow searching for owners by last name.
- **FR-005**: System SHOULD display a list of pets associated with an owner.
- **FR-006**: System MUST enforce that owner's first name is not blank.
- **FR-007**: System MUST enforce that owner's last name is not blank.
- **FR-008**: System MUST enforce that owner's address is not blank.
- **FR-009**: System MUST enforce that owner's city is not blank.
- **FR-010**: System MUST enforce that owner's telephone number is exactly 10 digits.
- **FR-011**: System MUST enforce that pet's name is not blank.
- **FR-012**: System MUST enforce that a pet's name is unique within an owner.
- **FR-013**: System MUST enforce that visit description is not blank.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including address, city, and telephone number. Has a one-to-many relationship with `Pet`.
- **Pet**: Represents a pet, including its name, birth date, and type. Has a many-to-one relationship with `PetType` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the type of a pet (e.g., cat, dog).
- **Visit**: Represents a visit to the clinic for a pet, including a date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find an owner by last name in under 3 seconds.
- **SC-002**: The system can display a list of all owners when no last name is provided in the search, within 5 seconds.
- **SC-003**: 95% of pet creation/update operations complete successfully with valid data.
- **SC-004**: Validation errors for owner and pet data are displayed clearly to the user within 1 second of submission.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing authentication mechanisms if applicable (though not explicitly detailed in the provided context).
- Data retention policies for owner and pet information will follow industry-standard practices for veterinary clinics.
- The primary interface for interacting with owner data will be a web-based application.
- The system will use standard date formats (yyyy-MM-dd) for pet birth dates and visit dates.