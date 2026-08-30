# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `025-owners-spring-petclinic`

**Created**: 2026-08-29

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for managing pet owners and is essential for basic operations.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and verifying redirection to the correct owner's detail page. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** an owner named "John Franklin" exists, **When** the user searches for owners with the last name "Franklin", **Then** the system displays the details for John Franklin.
2. **Given** multiple owners with the last name "Franklin" exist, **When** the user searches for owners with the last name "Franklin", **Then** the system displays a list of all owners with the last name "Franklin".

---

### User Story 2 - Find Owners with Partial Last Name Match (Priority: P2)

Given multiple owners whose last names start with "Frank" exist, When a user searches for owners with the last name "Frank", Then a list of owners is displayed.

**Why this priority**: Provides flexibility in searching and helps users find owners when they don't know the exact last name.

**Independent Test**: Can be fully tested by searching for a partial last name like "Frank" and verifying that all owners whose last names start with "Frank" are displayed. Delivers improved search usability.

**Acceptance Scenarios**:

1. **Given** owners "John Franklin" and "Jane Franks" exist, **When** the user searches for owners with the last name "Frank", **Then** both "John Franklin" and "Jane Franks" are displayed in the search results.

---

### User Story 3 - Handle Empty Last Name Search (Priority: P3)

Given multiple owners exist, When a user searches for owners with an empty last name (or whitespace), Then a list of all owners is displayed.

**Why this priority**: Ensures that a search with no criteria returns all available data, which is a common and expected behavior.

**Independent Test**: Can be fully tested by leaving the last name search field blank and submitting the search, then verifying that all existing owners are listed. Delivers a comprehensive view of all owners.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** the user searches for owners with an empty last name, **Then** all owners in the system are displayed.

---

### Edge Cases

- What happens when an owner's address is blank? → Validation error is shown, and the owner cannot be saved.
- What happens when an owner's city is blank? → Validation error is shown, and the owner cannot be saved.
- How does system handle an invalid telephone format (not 10 digits)? → Validation error is shown, and the owner cannot be saved.
- What happens when attempting to access an owner with a non-existent ID? → An "owner not found" error is displayed.
- What happens when creating a pet with a blank name? → Validation error is shown, and the pet cannot be saved.
- What happens when creating a pet with a missing type? → Validation error is shown, and the pet cannot be saved.
- What happens when creating a pet with an invalid birth date? → Validation error is shown, and the pet cannot be saved.
- What happens when attempting to save a pet with a name that already exists for the same owner? → Validation error is shown, and the pet cannot be saved.
- What happens when creating a visit with an invalid date (not after current date)? → Validation error is shown, and the visit cannot be saved.
- What happens when attempting to create a visit for a pet that does not exist for a given owner? → An "pet not found" error is displayed.
- What happens when searching for owners by last name when no owners match? → A "not found" message is displayed.
- What happens when navigating to the "/oups" endpoint? → A runtime exception is thrown to demonstrate error handling.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow finding owners by last name.
- **FR-005**: System SHOULD allow inserting a new owner.
- **FR-006**: System MUST ensure owner's address is not blank.
- **FR-007**: System MUST ensure owner's city is not blank.
- **FR-008**: System MUST ensure owner's telephone is exactly 10 digits.
- **FR-009**: System MUST ensure owner's first name is not blank.
- **FR-010**: System MUST ensure owner's last name is not blank.
- **FR-011**: System MUST ensure pet's name is not blank.
- **FR-012**: System MUST ensure visit description is not blank.
- **FR-013**: System MUST ensure a pet's name is unique within an owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their personal details (address, city, telephone) and a collection of associated pets.
- **Pet**: Represents a pet, including its name, birth date, type, and associated visits.
- **PetType**: Represents the classification of a pet (e.g., dog, cat).
- **Visit**: Represents a record of a pet's visit to the clinic, including the date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 2 seconds.
- **SC-002**: System supports managing up to 1000 owners and their associated pets without performance degradation.
- **SC-003**: 95% of owner and pet data entry operations complete successfully on the first attempt.
- **SC-004**: Reduce support inquiries related to owner and pet data management by 30%.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication mechanisms will be leveraged if applicable to owner management.
- Data validation rules are applied consistently across all entry points.
- The system will use a relational database for persistence.