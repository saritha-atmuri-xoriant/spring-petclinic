# Feature Specification: Owner Management

**Feature Branch**: `008-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given owners exist in the system, When a user searches for owners by a last name starting with "Franklin", Then the system should display a list of owners whose last names start with "Franklin" and redirect to the owner's detail page.

**Why this priority**: This is a core functionality for navigating and managing existing owner data, essential for daily operations.

**Independent Test**: Can be fully tested by entering "Franklin" into the owner search field and verifying the correct owners are displayed and the detail page is accessible.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Franklin", "Frank", and "Smith", **When** a user searches for owners with the last name "Frank", **Then** the system displays a list containing "Franklin" and "Frank", and the user can navigate to the detail page of any displayed owner.
2. **Given** there are no owners with the last name "Zebra", **When** a user searches for owners with the last name "Zebra", **Then** the system displays a message indicating no owners were found.

---

### User Story 2 - Create a New Owner (Priority: P2)

Given a user is on the new owner form, When they submit a valid owner form with all required fields, Then the owner is created and a success message is displayed.

**Why this priority**: Enabling new owner registration is crucial for onboarding new clients to the pet clinic.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner is added to the system and a confirmation is shown.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they enter a valid first name, last name, address, city, telephone number, and submit the form, **Then** the new owner is successfully created and displayed in the owner list, and a success message is shown.

---

### User Story 3 - Handle Invalid Owner Creation (Priority: P3)

Given a user is on the new owner form, When they submit the form with errors, Then the system displays an error message and returns to the owner creation form.

**Why this priority**: Providing clear feedback on invalid input is important for user experience and data integrity.

**Independent Test**: Can be fully tested by submitting the new owner form with missing or invalid data and verifying error messages are displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they leave the first name blank and submit the form, **Then** an error message "First name must not be blank" is displayed next to the first name field, and the form remains open.
2. **Given** a user is on the "Add Owner" form, **When** they enter a telephone number with 9 digits and submit the form, **Then** an error message "Telephone must be exactly 10 digits" is displayed next to the telephone field, and the form remains open.

---

### Edge Cases

- What happens when an owner's telephone number is not exactly 10 digits? → Validation error.
- How does the system handle an attempt to create an owner with a non-existent Pet ID for a visit? → `IllegalArgumentException` is thrown.
- What happens when a pet's name is not unique within an owner? → Validation error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow updating an existing owner's details.
- **FR-003**: System MUST validate that the owner's first name is not blank.
- **FR-004**: System MUST validate that the owner's last name is not blank.
- **FR-005**: System MUST validate that the owner's address is not blank.
- **FR-006**: System MUST validate that the owner's city is not blank.
- **FR-007**: System MUST validate that the owner's telephone number is exactly 10 digits.
- **FR-008**: System MUST allow finding owners by last name.
- **FR-009**: System MUST allow viewing an owner's details, including their pets and visits.
- **FR-010**: System MUST allow the creation of new pets for an owner.
- **FR-011**: System MUST allow updating an existing pet's name.
- **FR-012**: System SHOULD validate pet information during creation or update.
- **FR-013**: System SHOULD display a form for creating or updating a pet.
- **FR-014**: System SHOULD allow finding owners by last name.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents a pet belonging to an owner. Key attributes include name, birth date, and type. A pet can have multiple visits.
- **PetType**: Represents the type of pet (e.g., Cat, Dog).
- **Visit**: Represents a visit to the clinic for a pet. Key attributes include date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully create a new owner profile in under 1 minute.
- **SC-002**: Searching for owners by last name returns results in under 2 seconds.
- **SC-003**: 95% of users can successfully add a new pet to an existing owner's profile on their first attempt.
- **SC-004**: Validation errors for owner creation are displayed clearly and immediately upon form submission, leading to a 90% reduction in invalid owner submissions.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse the existing authentication and authorization mechanisms.
- Data retention policies for owner information will follow industry standards for veterinary clinics.
- The primary interface for managing owners will be a web-based application.