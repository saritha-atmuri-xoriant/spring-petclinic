# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `052-owners-spring-petclinic`

**Created**: 2026-08-30

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing the clinic's client base and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the displayed list of owners.

**Acceptance Scenarios**:

1. **Given** there are multiple owners in the system with last names like "Smith", "Smythe", and "Jones", **When** a user searches for owners with the last name prefix "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** there are no owners with the last name "Xyz", **When** a user searches for owners with the last name prefix "Xyz", **Then** a "No owners found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P2)

As a clinic staff member, I want to add new owners to the system so that I can register new clients and their pets.

**Why this priority**: Essential for onboarding new clients and expanding the clinic's customer base.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying that the owner is created and their details page is displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the "New Owner" form, **When** they enter valid owner details (first name, last name, address, city, telephone) and submit the form, **Then** the owner is successfully created and the user is redirected to the owner's details page.
2. **Given** a user is on the "New Owner" form, **When** they attempt to submit the form with a blank required field (e.g., last name), **Then** a validation error message is displayed for the blank field, and the form remains on the page without creating the owner.

---

### User Story 3 - Handle Duplicate Pet Name for the Same Owner (Priority: P3)

As a clinic staff member, I want the system to prevent me from adding a pet with a name that already exists for the same owner, so that pet records are unique and manageable.

**Why this priority**: Ensures data integrity and prevents confusion when managing multiple pets for a single owner.

**Independent Test**: Can be fully tested by attempting to add a second pet with the same name to an owner who already has a pet with that name.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" has a pet named "Buddy", **When** an attempt is made to add a new pet for "John Doe" with the name "Buddy", **Then** an error message "This pet name already exists for this owner" is displayed, and the create/update pet form remains on the page.

---

### Edge Cases

- What happens when an owner's telephone number does not match the 10-digit pattern? → Validation error.
- How does the system handle an attempt to edit an owner whose ID does not exist? → `IllegalArgumentException` is thrown.
- What happens when a user attempts to create a pet for an owner ID that does not exist? → `IllegalArgumentException` is thrown.
- How does the system handle an attempt to create a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` is thrown.
- What happens when a pet's name is blank during creation or update? → Validation error.
- How does the system handle an attempt to create or update an owner with an ID field provided? → The ID field is disallowed.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone number.
- **FR-002**: System MUST allow the search for owners by last name prefix.
- **FR-003**: System MUST display a list of owners matching the provided last name prefix.
- **FR-004**: System MUST allow the creation of a new pet for an existing owner, including pet name, birth date, and pet type.
- **FR-005**: System MUST prevent the creation of a pet with a name that already exists for the same owner.
- **FR-006**: System MUST allow the update of an existing pet's name.
- **FR-007**: System MUST validate owner information during creation or update, enforcing non-blank fields for first name, last name, address, and city, and a 10-digit pattern for the telephone number.
- **FR-008**: System MUST validate pet information during creation or update, enforcing non-blank pet name and a valid birth date.
- **FR-009**: System MUST disallow the ID field when creating or updating an owner.
- **FR-010**: System MUST disallow the ID field when creating or updating a visit.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (name, address, city, telephone) and a collection of associated pets.
- **Pet**: Represents a pet, including its name, birth date, type, and owner.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a veterinary visit for a pet, including the date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 3 seconds.
- **SC-002**: New owners can be successfully created and displayed within 5 seconds of form submission.
- **SC-003**: 95% of attempts to create a duplicate pet name for the same owner result in a clear validation error message.
- **SC-004**: All mandatory fields for owner creation are validated, with validation errors appearing within 1 second of form submission.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing authentication mechanisms for staff users.
- Data retention policies for owner and pet information will follow standard industry practices for veterinary clinics.
- The system will use standard web application patterns for form submissions and data display.