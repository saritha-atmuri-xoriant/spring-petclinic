# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `004-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for navigating the application and finding specific owner information.

**Independent Test**: Can be fully tested by entering "Franklin" in the search field and verifying navigation to the correct owner's detail page.

**Acceptance Scenarios**:

1. **Given** an owner named "John Franklin" exists, **When** the user searches for "Franklin", **Then** the system displays the details for John Franklin.
2. **Given** multiple owners with the last name "Smith" exist, **When** the user searches for "Smith", **Then** the system displays a list of all owners with the last name "Smith".

---

### User Story 2 - Find Owners with Partial Last Name (Priority: P2)

Given owners exist with last names starting with "F", When a user searches for owners with the last name "F", Then a list of owners whose last names start with "F" is displayed.

**Why this priority**: Allows for flexible searching and discovery of owners.

**Independent Test**: Can be tested by entering a partial last name like "F" and verifying that all owners whose last names start with "F" are displayed.

**Acceptance Scenarios**:

1. **Given** owners "Alice Franklin", "Bob Foster", and "Charlie Davis" exist, **When** the user searches for "F", **Then** the system displays "Alice Franklin" and "Bob Foster".

---

### User Story 3 - Handle Empty Search for Last Name (Priority: P3)

Given multiple owners exist, When a user searches for owners with an empty last name (or only whitespace), Then all owners are displayed in the owner list.

**Why this priority**: Ensures a graceful fallback for incomplete search queries.

**Independent Test**: Can be tested by submitting an empty search query and verifying that all owners are listed.

**Acceptance Scenarios**:

1. **Given** multiple owners exist, **When** the user searches with an empty last name field, **Then** all owners are displayed.

---

### User Story 4 - Create New Owner (Priority: P1)

Given a user wants to add a new pet owner, When the user provides valid owner details (first name, last name, address, city, telephone), Then a new owner record is created.

**Why this priority**: Essential for onboarding new clients into the system.

**Independent Test**: Can be tested by filling out the new owner form with valid data and verifying the owner is added to the system.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they enter valid details for "Jane Doe", "123 Main St", "Anytown", and "1234567890", **Then** Jane Doe is added as a new owner.

---

### User Story 5 - Update Existing Owner (Priority: P2)

Given an existing owner's details need to be modified, When the user updates the owner's information (address, city, telephone), Then the owner's record is updated.

**Why this priority**: Allows for maintaining accurate owner information.

**Independent Test**: Can be tested by selecting an existing owner, modifying their details, and verifying the changes are saved.

**Acceptance Scenarios**:

1. **Given** an owner "John Franklin" exists with address "456 Oak Ave", **When** the user updates the address to "789 Pine Ln", **Then** John Franklin's address is updated to "789 Pine Ln".

---

### User Story 6 - Add Pet to Owner (Priority: P1)

Given an existing owner, When the user adds a new pet for that owner with a name and birth date, Then the pet is associated with the owner.

**Why this priority**: Core functionality for managing a pet owner's pets.

**Independent Test**: Can be tested by selecting an owner, adding a new pet with valid details, and verifying the pet appears under the owner.

**Acceptance Scenarios**:

1. **Given** owner "Jane Doe" exists, **When** the user adds a pet named "Buddy" with birth date "2023-01-15", **Then** "Buddy" is listed as a pet for "Jane Doe".

---

### User Story 7 - Add Visit to Pet (Priority: P1)

Given an existing pet, When the user adds a new visit for that pet with a date, Then the visit is recorded for the pet.

**Why this priority**: Essential for tracking pet health history.

**Independent Test**: Can be tested by selecting a pet, adding a visit with a valid date, and verifying the visit is recorded.

**Acceptance Scenarios**:

1. **Given** pet "Buddy" (owned by Jane Doe) exists, **When** the user adds a visit on "2024-03-10", **Then** a visit on "2024-03-10" is recorded for "Buddy".

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error "required".
- **Missing Pet Type**: Pet creation with a missing pet type → validation error "required".
- **Invalid Pet Birth Date Format**: Pet update with a birth date in an incorrect format (e.g., "2015/02/12") → validation error "typeMismatch".
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error "duplicate".
- **Blank Visit Date**: Visit creation with a blank date → validation error.
- **Visit Date Not in Future**: Visit creation with a date that is not after the current date → validation error "typeMismatch.visitDate".
- **Non-existent Owner ID for Visit**: Attempting to add a visit for a pet belonging to a non-existent owner → `IllegalArgumentException` is thrown.
- **Non-existent Pet ID for Visit**: Attempting to add a visit for a non-existent pet belonging to an owner → `IllegalArgumentException` is thrown.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow updating an existing owner's address, city, and telephone.
- **FR-003**: System MUST allow finding owners by last name, including partial matches.
- **FR-004**: System MUST display all owners when a search for an empty last name is performed.
- **FR-005**: System MUST allow the creation of a new pet for an existing owner, including pet name and birth date.
- **FR-006**: System MUST allow updating an existing pet's name and birth date.
- **FR-007**: System MUST allow adding new visits for a pet, including the visit date.
- **FR-008**: System MUST validate owner details upon creation and update, enforcing non-blank fields for first name, last name, address, and city, and a 10-digit format for telephone.
- **FR-009**: System MUST validate pet details upon creation and update, enforcing non-blank pet name and a valid birth date format.
- **FR-010**: System MUST prevent duplicate pet names for the same owner.
- **FR-011**: System MUST validate visit details upon creation, enforcing a non-blank date and a date in the future.
- **FR-012**: System MUST handle attempts to edit or view non-existent owners by throwing an `IllegalArgumentException`.
- **FR-013**: System MUST handle attempts to add visits for non-existent owners or pets by throwing an `IllegalArgumentException`.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Attributes include first name, last name, address, city, and telephone number. Has a one-to-many relationship with `Pet`.
- **Pet**: Represents a pet. Attributes include name, birth date, and type. Has a many-to-one relationship with `Owner` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the type of pet (e.g., Cat, Dog). Attributes include name.
- **Visit**: Represents a visit to the clinic. Attributes include date and description. Has a many-to-one relationship with `Pet`.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation and updates are completed within 5 seconds.
- **SC-003**: Adding a new pet or visit for an owner is completed within 5 seconds.
- **SC-004**: 99% of owner, pet, and visit data entries pass validation checks.
- **SC-005**: System handles 100 concurrent users performing owner-related operations without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- The system will use a relational database for data persistence.
- Standard date and time formats will be used for input and display.
- Error messages will be user-friendly and informative.
- The system will be deployed in a secure environment.
- The `PetType` entity will be pre-populated with common pet types.
- The system will use a standard session-based authentication mechanism.
- The `Visit` entity will have a description field for visit details.