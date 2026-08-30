# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `047-owners-spring-petclinic`

**Created**: 2026-08-30

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given owners exist in the system, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for managing and locating pet owners, essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the displayed list of owners. Delivers the ability to quickly find specific owners.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for owners with the last name prefix "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** there are no owners with the last name "Davis", **When** the user searches for owners with the last name prefix "Dav", **Then** a message indicating "No owners found" is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: Essential for onboarding new clients into the pet clinic system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, and submitting. Verifies the creation and redirection.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they fill in the first name, last name, address, city, and telephone number with valid data, and click "Save", **Then** the new owner is created and the user is redirected to the owner's details page.

---

### User Story 3 - View Owner List (Priority: P2)

Given owners exist in the system, When a user navigates to the owners list page, Then all owners are displayed.

**Why this priority**: Provides an overview of all registered owners, useful for administrative tasks and general reference.

**Independent Test**: Can be fully tested by navigating to the owners list page and verifying that all existing owners are displayed.

**Acceptance Scenarios**:

1. **Given** there are three owners registered in the system, **When** the user navigates to the "Owners" list page, **Then** all three owners are displayed in a list format.

---

### User Story 4 - Edit an Existing Owner (Priority: P2)

Given an owner exists in the system, When a user navigates to the owner's details page and chooses to edit, Then they can update the owner's information and save the changes.

**Why this priority**: Allows for maintaining accurate owner information as it changes over time.

**Independent Test**: Can be fully tested by selecting an owner, navigating to their edit page, modifying a field, saving, and verifying the update on the details page.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" exists with address "123 Main St", **When** the user navigates to John Doe's details, clicks "Edit", changes the address to "456 Oak Ave", and clicks "Save", **Then** John Doe's details page now shows the address as "456 Oak Ave".

---

### User Story 5 - Add a Pet to an Owner (Priority: P3)

Given an owner exists, When a user navigates to the owner's details page and chooses to add a pet, Then they can enter pet details and associate it with the owner.

**Why this priority**: Core functionality for managing a pet owner's associated pets.

**Independent Test**: Can be fully tested by selecting an owner, navigating to their pet addition form, entering valid pet details, and saving. Verifies the pet is linked to the owner.

**Acceptance Scenarios**:

1. **Given** owner "Jane Smith" exists, **When** the user navigates to Jane Smith's details, clicks "Add Pet", enters pet name "Buddy", birth date "2022-05-15", and pet type "Dog", and clicks "Save", **Then** "Buddy" is listed as one of Jane Smith's pets.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → validation error.
- **Non-existent Owner ID**: Attempting to edit or access details for a non-existent owner ID → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation with a missing pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation/update with an invalid birth date format → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Visit creation with a date that is not in the future → validation error.
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a non-existent pet ID for a given owner → `IllegalArgumentException` is thrown.
- **Missing Owner for Pet Operations**: Attempting to perform pet or visit operations for a non-existent owner ID → `IllegalArgumentException` is thrown.
- **No Owners Found**: Searching for owners with a last name that yields no results → validation error on `lastName` field.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new pets for an owner.
- **FR-002**: System MUST allow updating an existing pet's name.
- **FR-003**: System SHOULD validate pet data during creation or update.
- **FR-004**: System SHOULD allow searching for owners by last name.
- **FR-005**: System SHOULD display a list of pets associated with an owner.
- **FR-006**: System MUST allow the creation of new owners.
- **FR-007**: System MUST allow updating an existing owner's details (address, city, telephone).
- **FR-008**: System MUST display a list of all owners.
- **FR-009**: System MUST display an owner's details, including their pets.
- **FR-010**: System MUST validate owner data during creation or update.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Includes address, city, telephone, and a collection of associated pets.
- **Pet**: Represents a pet belonging to an owner. Includes birth date, type, and a collection of visits.
- **PetType**: Represents the type of a pet (e.g., cat, dog).
- **Visit**: Represents a visit to the vet for a pet. Includes a date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 3 seconds.
- **SC-002**: New owners can be created with all required fields in under 1 minute.
- **SC-003**: The owner list page loads displaying all owners within 5 seconds.
- **SC-004**: 95% of owner data updates are successfully saved and reflected immediately.
- **SC-005**: 90% of users can successfully add a new pet to an owner on their first attempt.

## Assumptions

- Users have stable internet connectivity.
- The system will be used by clinic staff with appropriate permissions.
- Data validation messages will be user-friendly and informative.
- The primary language for the application is English.
- The system will reuse existing Person class attributes for owner first and last names.