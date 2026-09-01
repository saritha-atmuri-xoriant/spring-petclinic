# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `009-owners-spring-petclinic`

**Created**: 2026-09-01

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for managing pet owners and is essential for basic system operation.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and verifying redirection to the correct owner's detail page.

**Acceptance Scenarios**:

1. **Given** an owner named "John Franklin" exists in the system, **When** a user searches for owners with the last name "Franklin", **Then** the system displays the details page for John Franklin.

---

### User Story 2 - Find Owners with Partial Last Name Match (Priority: P2)

Given multiple owners whose last names start with "Frank" exist, When a user searches for owners with the last name "Frank", Then a list of owners is displayed.

**Why this priority**: This enhances user experience by allowing for more flexible searching, which is important for usability.

**Independent Test**: Can be fully tested by searching for a partial last name like "Frank" and verifying that all owners whose last names start with "Frank" are displayed in a list.

**Acceptance Scenarios**:

1. **Given** owners "John Franklin" and "Jane Franks" exist, **When** a user searches for owners with the last name "Frank", **Then** a list containing both "John Franklin" and "Jane Franks" is displayed.

---

### User Story 3 - Handle Empty Last Name Search (Priority: P3)

Given multiple owners exist, When a user searches for owners with an empty or whitespace-only last name, Then all owners are displayed.

**Why this priority**: This ensures the system behaves predictably and doesn't break when users perform incomplete searches.

**Independent Test**: Can be fully tested by leaving the last name search field empty and submitting the search, then verifying that all existing owners are displayed.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** a user searches for owners with an empty last name field, **Then** all owners are displayed.

---

### Edge Cases

- What happens when an owner's telephone number does not match the `\d{10}` pattern?
- How does the system handle attempts to create or update a pet with a name that already exists for the same owner?
- What happens when a user attempts to add a visit for a pet ID that does not exist for a given owner?

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with address, city, and telephone.
- **FR-002**: System MUST allow the updating of an existing owner's details (address, city, telephone).
- **FR-003**: System MUST allow the creation of a new pet for an existing owner, including birth date and type.
- **FR-004**: System MUST allow the updating of an existing pet's details (name, birth date, type).
- **FR-005**: System MUST allow the retrieval of all pet types for pet creation.
- **FR-006**: System MUST validate owner information during creation or update, enforcing non-blank fields for first name, last name, address, city, and a 10-digit telephone number.
- **FR-007**: System MUST validate pet information during creation or update, enforcing non-blank pet name and a valid pet type.
- **FR-008**: System MUST prevent duplicate pet names for the same owner.
- **FR-009**: System MUST handle potential data integrity violations when saving owner or pet data.
- **FR-010**: System MUST allow searching for owners by last name, supporting exact and partial matches.
- **FR-011**: System MUST display all owners when a search for an empty last name is performed.
- **FR-012**: System MUST display an error message when attempting to find an owner with a non-existent ID.
- **FR-013**: System MUST display a "notFound" validation error for the "lastName" field when a search yields no results.
- **FR-014**: System MUST allow the creation of a new visit for an existing pet, including a date.
- **FR-015**: System MUST validate visit date to ensure it is not in the past.
- **FR-016**: System MUST throw an `IllegalArgumentException` when attempting to add a visit for a non-existent pet ID.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Includes address, city, telephone, and a list of associated pets.
- **Pet**: Represents a pet belonging to an owner. Includes birth date and type. Associated with visits.
- **PetType**: Represents the type of a pet (e.g., cat, dog).
- **Visit**: Represents a visit to the vet for a pet. Includes a date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully search for and view owner details within 3 seconds.
- **SC-002**: The system correctly displays a list of owners for partial last name searches 99% of the time.
- **SC-003**: Owner and pet creation/update operations complete successfully with valid data in under 5 seconds.
- **SC-004**: Validation errors are displayed clearly and accurately for all invalid owner and pet data inputs.
- **SC-005**: The system prevents duplicate pet names for the same owner with 100% accuracy.
- **SC-006**: Visit creation for existing pets completes successfully within 4 seconds.
- **SC-007**: The system correctly handles and reports errors for invalid visit dates.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing Person and BaseEntity/NamedEntity structures.
- Data persistence will be handled by Spring Data JPA repositories.
- Validation will leverage Jakarta Bean Validation annotations.
- The primary interface for interacting with owners will be a web-based UI.
- The date format for birth dates and visit dates will be "yyyy-MM-dd".
- The telephone number format is strictly 10 digits.