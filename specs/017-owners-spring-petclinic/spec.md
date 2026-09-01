# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `017-owners-spring-petclinic`

**Created**: 2026-03-19

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing owners and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search form and verifying the returned list of owners.

**Acceptance Scenarios**:

1. **Given** there are owners in the system, **When** a user searches for owners by the last name prefix "Sm", **Then** a list of owners whose last names start with "Sm" (e.g., Smith, Smothers) is displayed.
2. **Given** there are no owners with a specific last name prefix, **When** a user searches for owners by that prefix, **Then** a "No owners found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P2)

As a clinic staff member, I want to create a new owner profile so that I can register new clients.

**Why this priority**: Essential for onboarding new clients into the system.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying that the owner is created and their details page is displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields filled correctly, **Then** the owner is created and the user is redirected to the newly created owner's details page.

---

### User Story 3 - Update Owner Details (Priority: P3)

As a clinic staff member, I want to update an existing owner's details so that their information remains current.

**Why this priority**: Ensures data accuracy for existing clients.

**Independent Test**: Can be fully tested by selecting an existing owner, modifying their details, saving the changes, and verifying that the updated information is displayed on their profile.

**Acceptance Scenarios**:

1. **Given** an owner exists in the system, **When** the owner's telephone number is updated and saved, **Then** the changes are persisted and the new telephone number is reflected on the owner's profile.

---

### Edge Cases

- What happens when an owner is created or updated with a blank first name? → Validation error.
- What happens when an owner is created or updated with a blank last name? → Validation error.
- What happens when an owner is created or updated with an invalid telephone number format (not 10 digits)? → Validation error.
- What happens when an owner is created or updated with a blank address? → Validation error.
- What happens when an owner is created or updated with a blank city? → Validation error.
- What happens when attempting to edit or view an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when attempting to create a visit for an owner ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when attempting to create a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` is thrown.
- What happens when submitting the owner find form without a last name? → A broad search is performed.
- What happens when navigating to the `/oups` endpoint? → A `RuntimeException` is thrown, resulting in an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow updating an existing owner's details (address, city, telephone).
- **FR-003**: System MUST allow searching for owners by last name prefix.
- **FR-004**: System MUST display a list of owners matching the search criteria.
- **FR-005**: System MUST display a form for creating new owner details.
- **FR-006**: System MUST display a form for updating existing owner details.
- **FR-007**: System MUST validate owner information during creation and update according to defined business rules.
- **FR-008**: System MUST allow the creation of new pets for an owner.
- **FR-009**: System MUST allow updating an existing pet's name.
- **FR-010**: System SHOULD validate pet information during creation or update.
- **FR-011**: System SHOULD display a form for creating or updating pet details.
- **FR-012**: System SHOULD populate a list of available pet types for selection during pet creation/update.
- **FR-013**: System MUST allow the creation of new visits for a pet.
- **FR-014**: System MUST validate visit information during creation.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Attributes include first name, last name, address, city, and telephone number. Has a one-to-many relationship with `Pet`.
- **Pet**: Represents a pet. Attributes include name, birth date, and type. Has a many-to-one relationship with `Owner` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the type of pet (e.g., Cat, Dog). Attributes include name.
- **Visit**: Represents a visit to the clinic for a pet. Attributes include date and description. Has a many-to-one relationship with `Pet`.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 3 seconds.
- **SC-002**: New owner creation is completed successfully for 99% of valid submissions.
- **SC-003**: Owner detail updates are reflected immediately upon saving.
- **SC-004**: The system supports up to 500 concurrent users performing owner management operations without performance degradation.

## Assumptions

- Users performing owner management operations are clinic staff with appropriate permissions.
- The system will reuse existing validation logic for names, addresses, and cities.
- The telephone number format validation (`\d{10}`) is sufficient for current needs.
- Pet creation and update forms will include a dropdown for selecting `PetType`.
- Visit creation will include a date picker and a text field for description.
- The system will handle non-existent owner or pet IDs gracefully by returning appropriate error messages or exceptions.