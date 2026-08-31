# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `007-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly access their information and their pets' details.

**Why this priority**: This is a core functionality for managing owner information and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name in the search field and verifying the returned list of owners.

**Acceptance Scenarios**:

1. **Given** a list of owners exists in the system, **When** a user searches for owners by the last name "Davis", **Then** a list of owners whose last name starts with "Davis" is displayed.
2. **Given** a list of owners exists in the system, **When** a user searches for an owner last name that does not exist, **Then** a "no owners found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a new user, I want to create a new owner profile so that I can register myself and my pets with the clinic.

**Why this priority**: This is fundamental for onboarding new clients to the clinic.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner is created and redirected to their details page.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields filled, **Then** the owner is created and the user is redirected to the owner's details page.
2. **Given** a user is on the new owner form, **When** they submit the form with a blank required field (e.g., last name), **Then** a validation error is shown for the blank field, and the owner is not created.

---

### User Story 3 - Add a New Pet for an Existing Owner (Priority: P2)

As a pet owner, I want to add a new pet to my existing owner profile so that I can register all my pets with the clinic.

**Why this priority**: Allows owners to manage their complete pet roster.

**Independent Test**: Can be fully tested by navigating to an owner's details page, initiating the "add pet" action, filling out the pet form, and verifying the pet is added.

**Acceptance Scenarios**:

1. **Given** an existing owner is logged in, **When** they navigate to their profile and choose to add a new pet, **And** they fill in all required pet details (name, birth date, type), **Then** the new pet is successfully added to the owner's profile.
2. **Given** an existing owner is logged in, **When** they attempt to add a new pet with a name that already exists for that owner, **Then** a validation error is shown indicating the pet name is a duplicate, and the pet is not added.

---

### User Story 4 - Update an Existing Pet's Information (Priority: P2)

As a pet owner, I want to update the information for an existing pet (name, birth date, type) so that my pet's records are accurate.

**Why this priority**: Ensures pet records are up-to-date.

**Independent Test**: Can be fully tested by navigating to an owner's details page, selecting a pet to edit, changing its details, and verifying the changes are saved.

**Acceptance Scenarios**:

1. **Given** an existing owner has a pet registered, **When** the owner navigates to edit that pet's details and changes the pet's name, **Then** the pet's name is updated successfully.
2. **Given** an existing owner has a pet registered, **When** the owner navigates to edit that pet's details and changes the pet's type, **Then** the pet's type is updated successfully.

---

### User Story 5 - Add a New Visit for a Pet (Priority: P3)

As a clinic staff member, I want to add a new visit record for a pet so that the pet's medical history is maintained.

**Why this priority**: Essential for tracking pet health and treatments.

**Independent Test**: Can be fully tested by navigating to a pet's details page, initiating the "add visit" action, filling out the visit details, and verifying the visit is recorded.

**Acceptance Scenarios**:

1. **Given** a pet is registered with the clinic, **When** a user navigates to the pet's details and adds a new visit with a valid date and description, **Then** the visit is successfully recorded for that pet.
2. **Given** a pet is registered with the clinic, **When** a user attempts to add a visit with an invalid date format, **Then** a validation error is shown, and the visit is not recorded.

---

### Edge Cases

- What happens when an owner is created or updated with a blank first name? → Validation error.
- What happens when an owner is created or updated with a blank last name? → Validation error.
- What happens when an owner is created or updated with a telephone number that does not match the `\\d{10}` pattern? → Validation error.
- What happens when an owner is created or updated with a blank address? → Validation error.
- What happens when an owner is created or updated with a blank city? → Validation error.
- What happens when an attempt is made to edit or view an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when searching for owners with a last name that yields no results? → System displays a "not found" error message.
- What happens when creating or updating a pet with a blank name? → Validation error "required".
- What happens when creating a pet without selecting a pet type? → Validation error "required".
- What happens when creating or updating a pet with a birth date in an incorrect format (e.g., "2015/02/12")? → Validation error "typeMismatch".
- What happens when attempting to save a pet with a name that already exists for the same owner? → Validation error "duplicate".
- What happens when booking a visit with a date that is not in the future? → Validation error "typeMismatch.visitDate".
- What happens when attempting to add a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` is thrown.
- What happens when validating a pet object with an empty name? → Validation error.
- What happens when validating a pet object with a null type? → Validation error.
- What happens when validating a pet object with a null birth date? → Validation error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the search for owners by last name.
- **FR-003**: System MUST allow the creation of a new pet for an existing owner.
- **FR-004**: System MUST allow the update of an existing pet's name, birth date, and type.
- **FR-005**: System SHOULD validate pet information (name, birth date, type) during creation or update.
- **FR-006**: System MUST allow adding new visits for a pet.
- **FR-007**: System SHOULD validate visit information (date, description) during creation.
- **FR-008**: System MUST enforce that an owner's first name, last name, address, city, and telephone number are not blank.
- **FR-009**: System MUST enforce that a pet's name is not blank.
- **FR-010**: System MUST enforce that a pet's name is unique for a given owner.
- **FR-011**: System MUST enforce that a visit's description is not blank.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (name, address, city, telephone) and a collection of associated pets.
- **Pet**: Represents a pet, including its name, birth date, and type, and is associated with an owner and a list of visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a medical visit for a pet, including the date and a description of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created successfully in under 1 minute.
- **SC-003**: Adding a new pet to an owner's profile is completed in under 45 seconds.
- **SC-004**: 95% of pet and owner data entry operations complete without validation errors when valid data is provided.
- **SC-005**: The system supports up to 50 concurrent users performing owner and pet management tasks without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- The underlying database is capable of storing and retrieving owner and pet information efficiently.
- Standard date and time formats will be used for input and display.
- The system will use a relational database for persistence.
- The application will be deployed in an environment where Spring Boot conventions can be followed.
- Internationalization (i18n) for user-facing strings will be handled according to the project constitution.