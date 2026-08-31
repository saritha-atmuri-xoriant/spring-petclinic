# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `[001-owners-for-spring-petclinic]`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system displays the owner's details page.

**Why this priority**: This is a core functionality for managing pet owners and is essential for basic system operation.

**Independent Test**: Can be fully tested by searching for an existing owner's last name and verifying the correct details page is displayed.

**Acceptance Scenarios**:

1. **Given** the system has an owner with the last name "Franklin", **When** a user navigates to the owner search page and enters "Franklin" in the last name field, **Then** the system redirects to the owner's details page for "Franklin".
2. **Given** the system has multiple owners with the last name "Franklin", **When** a user searches for "Franklin", **Then** the system displays a list of owners with the last name "Franklin".

---

### User Story 2 - Create a New Owner (Priority: P2)

Given a user is on the new owner form, When they submit a valid owner form with all required fields populated correctly, Then the owner is created and the user is redirected to the owner's details page.

**Why this priority**: Adding new owners is a fundamental operation for the pet clinic.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner is created and viewable.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they enter valid data for first name, last name, address, city, and telephone, **Then** the owner is successfully created and the user is redirected to the owner's details page.

---

### User Story 3 - Handle Invalid Owner Creation (Priority: P3)

Given a user is on the new owner form, When they submit an invalid owner form (e.g., missing required fields, invalid phone number), Then the system displays appropriate error messages for each invalid field and returns the user to the owner creation form.

**Why this priority**: Ensures data integrity and provides user feedback for incorrect input.

**Independent Test**: Can be fully tested by submitting the new owner form with various invalid data combinations and verifying error messages.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they submit the form with a blank first name, **Then** an error message "First name must not be blank" is displayed next to the first name field.
2. **Given** a user is on the "Add Owner" form, **When** they submit the form with a telephone number that is not 10 digits, **Then** an error message indicating an invalid telephone format is displayed.

---

### Edge Cases

- What happens when an owner is created or updated with a blank address? → Validation error.
- How does the system handle an attempt to add a pet with a name that already exists for the same owner? → Validation error "duplicate".
- What happens when a user tries to access the `/oups` endpoint? → A `RuntimeException` is thrown, resulting in an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone number.
- **FR-002**: System MUST allow finding owners by their last name.
- **FR-003**: System MUST validate that the owner's first name is not blank.
- **FR-004**: System MUST validate that the owner's last name is not blank.
- **FR-005**: System MUST validate that the owner's address is not blank.
- **FR-006**: System MUST validate that the owner's city is not blank.
- **FR-007**: System MUST validate that the owner's telephone number consists of exactly 10 digits.
- **FR-008**: System MUST allow the creation of a new pet for an existing owner, including pet name, birth date, and type.
- **FR-009**: System MUST validate that a pet's name is not blank.
- **FR-010**: System MUST validate that a pet's name is unique for a given owner.
- **FR-011**: System MUST allow the update of an existing pet's name.
- **FR-012**: System SHOULD validate pet information during creation or update.
- **FR-013**: System SHOULD allow adding a new visit for a pet, including visit date and description.
- **FR-014**: System MUST validate that a visit's description is not blank.
- **FR-015**: System MUST handle attempts to edit or view an owner with a non-existent ID by throwing an `IllegalArgumentException`.
- **FR-016**: System MUST handle attempts to add a visit for a pet that does not exist for the specified owner by throwing an `IllegalArgumentException`.
- **FR-017**: Accessing the `/oups` endpoint MUST result in a `RuntimeException`.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Includes address, city, telephone, and a collection of associated pets.
- **Pet**: Represents a pet belonging to an owner. Includes birth date, type, and a collection of visits.
- **PetType**: Represents the type of a pet (e.g., cat, dog).
- **Visit**: Represents a visit to the clinic for a pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name, with search results displayed in under 1 second.
- **SC-002**: New owners can be successfully created with all required fields in under 30 seconds.
- **SC-003**: Validation errors for owner creation are displayed immediately upon form submission, guiding the user to correct input.
- **SC-004**: 95% of pet creation/update operations complete successfully without validation errors when valid data is provided.
- **SC-005**: The system gracefully handles invalid owner IDs or pet IDs for owner association, preventing crashes and providing informative feedback.

## Assumptions

- Users have stable internet connectivity.
- The system will be used by clinic staff with appropriate permissions.
- Data retention policies for owner and pet information will follow standard industry practices unless otherwise specified.
- The primary interface for managing owners will be a web-based application.
- Existing authentication mechanisms will be leveraged if applicable to user roles.