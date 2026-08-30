# Feature Specification: Owner Management

**Feature Branch**: `033-owners-spring-petclinic`

**Created**: 2026-08-30

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find owners by last name (Priority: P1)

Given owners exist in the system, When a user searches for owners by a last name starting with "Franklin", Then the system displays a list of owners whose last names start with "Franklin" and redirects to the owner's detail page.

**Why this priority**: This is a core functionality for managing and retrieving existing owner information, essential for day-to-day operations.

**Independent Test**: Can be fully tested by entering "Franklin" in the owner search field and verifying the displayed results and navigation to the owner detail page.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Franklin", "Frank", and "Smith", **When** a user searches for owners by last name "Frank", **Then** the system displays owners with last names "Franklin" and "Frank".
2. **Given** there are no owners with the last name "NonExistent", **When** a user searches for owners by last name "NonExistent", **Then** the system displays an "Owner not found" message.

---

### User Story 2 - Create a new owner (Priority: P2)

Given a user is on the new owner form, When they submit a valid owner form with all required fields populated correctly, Then the owner is created and the user is redirected to the owner's detail page with a success indication.

**Why this priority**: Adding new owners is fundamental to growing the pet clinic's client base.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner is created and viewable.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit valid data for first name, last name, address, city, and telephone, **Then** the owner is successfully created and displayed on their detail page.

---

### User Story 3 - Update an existing owner (Priority: P2)

Given a user is viewing an owner's detail page, When they edit the owner's information and submit valid changes, Then the owner's details are updated and the updated information is displayed on the owner's detail page.

**Why this priority**: Allows for maintaining accurate and up-to-date owner information.

**Independent Test**: Can be fully tested by editing an existing owner's details and verifying the changes are saved and reflected.

**Acceptance Scenarios**:

1. **Given** an owner exists with specific details, **When** the user edits the owner's telephone number and saves, **Then** the owner's telephone number is updated to the new value.

---

### User Story 4 - Add a new pet to an owner (Priority: P3)

Given a user is viewing an owner's detail page, When they navigate to add a new pet and submit valid pet details, Then the new pet is associated with the owner and displayed on the owner's detail page.

**Why this priority**: Managing pets is a core aspect of the pet clinic's services.

**Independent Test**: Can be fully tested by navigating to an owner's page, adding a new pet, and verifying it appears under that owner.

**Acceptance Scenarios**:

1. **Given** an owner exists, **When** the user adds a new pet with a name, birth date, and type, **Then** the pet is successfully added to the owner's record.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` thrown.
- **No Owners Found**: Searching for owners with a last name that yields no results → error message "not found" displayed.
- **Blank Pet Name**: Creating or updating a pet with a blank name → validation error "required".
- **Missing Pet Type**: Creating or updating a pet without selecting a pet type → validation error "required".
- **Invalid Pet Birth Date Format**: Creating or updating a pet with a birth date in an invalid format (e.g., "2015/02/12") → validation error "typeMismatch".
- **Duplicate Pet Name for Same Owner**: Attempting to save a pet with a name that already exists for the same owner → validation error "duplicate".

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow users to create a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow users to search for owners by last name.
- **FR-003**: System MUST allow users to view the details of a specific owner, including their associated pets.
- **FR-004**: System MUST allow users to edit an existing owner's details (first name, last name, address, city, telephone).
- **FR-005**: System MUST allow users to create a new pet for an existing owner, including pet name, birth date, and type.
- **FR-006**: System MUST allow users to update an existing pet's information.
- **FR-007**: System SHOULD validate pet data before saving.
- **FR-008**: System SHOULD populate a list of available pet types when creating or updating a pet.
- **FR-009**: System SHOULD retrieve owner details when creating or updating a pet.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include first name, last name, address, city, and telephone. An owner can have multiple pets.
- **Pet**: Represents a pet. Key attributes include name, birth date, and type. A pet belongs to an owner and can have multiple visits.
- **PetType**: Represents the type of a pet (e.g., cat, dog).
- **Visit**: Represents a vet visit for a pet. Key attributes include date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created with all required fields in under 1 minute.
- **SC-003**: Existing owner details can be updated and reflected within 5 seconds.
- **SC-004**: New pets can be added to an owner's record in under 1 minute.
- **SC-005**: 95% of owner and pet data entries are valid according to defined business rules.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing Person and NamedEntity base classes for Owner and Pet respectively.
- The system will leverage Spring Data JPA for persistence.
- The telephone number format `\d{10}` is considered a reasonable default for a 10-digit number.
- The date format "yyyy-MM-dd" is the standard for birth dates and visit dates.
- The system will provide a dropdown or selection mechanism for Pet Types.
- The system will handle basic error messages for validation failures.