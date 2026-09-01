# Feature Specification: Owners for Spring-Petclinic

**Feature Branch**: `019-owners-spring-petclinic`

**Created**: 2026-09-01

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given owners exist in the system, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for basic system usability.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list of owners. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** a user searches for "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** there are no owners with the last name "Davis", **When** a user searches for "Davis", **Then** a "No owners found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P2)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: Adding new owners is fundamental to populating and expanding the system's data.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting the form, and verifying redirection to a newly created owner's detail page. Delivers the ability to add new individuals to the system.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they enter valid first name, last name, address, city, and telephone number, and click "Save", **Then** the owner is saved, and the user is redirected to the owner's details page.
2. **Given** a user is on the new owner form, **When** they leave the telephone number field blank, **Then** a validation error is shown for the telephone field, and the owner is not saved.

---

### User Story 3 - View Owner List (Priority: P3)

Given owners exist in the system, When a user navigates to the owners list page, Then all owners are displayed, paginated.

**Why this priority**: Provides an overview of all registered owners, useful for administrative tasks and general system monitoring.

**Independent Test**: Can be fully tested by navigating to the owner list page and verifying that a list of owners is displayed, with pagination controls if there are more owners than fit on a single page. Delivers a comprehensive view of all system owners.

**Acceptance Scenarios**:

1. **Given** there are 20 owners in the system and the page size is 10, **When** a user navigates to the owner list page, **Then** the first 10 owners are displayed, along with pagination controls to view the next set of owners.
2. **Given** there are no owners in the system, **When** a user navigates to the owner list page, **Then** a message indicating "No owners found" is displayed.

---

### Edge Cases

- What happens when an owner is created or updated with a blank address? → Validation error is displayed for the address field.
- What happens when an owner is created or updated with a blank city? → Validation error is displayed for the city field.
- What happens when an owner is created or updated with a telephone number that does not consist of exactly 10 digits? → Validation error is displayed for the telephone field.
- What happens when attempting to access or modify an owner with an ID that does not exist? → An appropriate error message indicating the owner was not found is displayed.
- What happens when a pet is created or updated with a blank name? → Validation error is displayed for the pet's name field.
- What happens when a pet is created with a missing pet type? → Validation error is displayed for the pet type field.
- What happens when a pet is created or updated with an invalid birth date (e.g., null)? → Validation error is displayed for the pet's birth date field.
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error is displayed indicating a duplicate pet name for the owner.
- What happens when a visit is created with a date that is not after the current date? → Validation error is displayed for the visit date field.
- What happens when attempting to create a visit for a pet that does not exist for a given owner? → An appropriate error message indicating the pet was not found for the owner is displayed.
- What happens when searching for owners with a last name that yields no results? → A validation error is displayed on the last name field indicating "notFound".

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new pets for an owner.
- **FR-002**: System MUST allow updating an existing pet's name.
- **FR-003**: System SHOULD validate pet data upon creation or update.
- **FR-004**: System SHOULD display a form for creating or updating pet information.
- **FR-005**: System SHOULD provide a list of available pet types for selection during pet creation.
- **FR-006**: System MUST allow the creation of new owners with their contact details (address, city, telephone).
- **FR-007**: System MUST allow updating existing owner details.
- **FR-008**: System MUST allow searching for owners by their last name.
- **FR-009**: System MUST display a list of all owners, with pagination.
- **FR-010**: System MUST allow the creation of new visits for a pet.
- **FR-011**: System MUST allow updating existing visit details.
- **FR-012**: System MUST validate owner data upon creation or update.
- **FR-013**: System MUST validate visit data upon creation or update.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual who owns one or more pets. Attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents an animal owned by an owner. Attributes include name, birth date, and type. A pet can have multiple visits.
- **PetType**: Represents the category of a pet (e.g., Cat, Dog, Hamster).
- **Visit**: Represents a veterinary visit for a pet. Attributes include date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully find owners by last name prefix in under 2 seconds.
- **SC-002**: New owners can be created with all required information in under 1 minute.
- **SC-003**: The owner list page loads and displays paginated results within 3 seconds.
- **SC-004**: 95% of users can successfully create a new pet for an existing owner on their first attempt.
- **SC-005**: System supports up to 500 concurrent users browsing the owner list without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing infrastructure for data persistence (e.g., database) is available and functional.
- The primary users of this feature are clinic staff.
- The system will use standard date and time formats for user input and display.
- The telephone number format validation will enforce a 10-digit numerical input.
- The system will provide user-friendly error messages for validation failures.