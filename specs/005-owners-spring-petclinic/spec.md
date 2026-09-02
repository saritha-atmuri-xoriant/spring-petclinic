# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `[001-owner-management]`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

**Description**: As a clinic staff member, I want to search for owners by their last name so that I can quickly find their information.

**Why this priority**: This is a core functionality for managing owner data and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the displayed list of owners.

**Acceptance Scenarios**:

1. **Given** there are owners in the system with last names "Smith", "Smythe", and "Jones", **When** a user searches for owners with the last name prefix "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** there are no owners with the last name "Doe", **When** a user searches for owners with the last name prefix "Doe", **Then** a "No owners found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

**Description**: As a new user, I want to create a new owner profile so that I can register myself or a new client with the clinic.

**Why this priority**: This is a fundamental requirement for onboarding new clients into the system.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying that the owner is created and their details page is displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the "New Owner" form, **When** they enter valid first name, last name, address, city, and a 10-digit telephone number, and submit the form, **Then** the owner is created and the user is redirected to the owner's details page.

---

### User Story 3 - View Owner List (Priority: P2)

**Description**: As a clinic staff member, I want to view a list of all owners so that I can get an overview of registered clients.

**Why this priority**: Provides a general overview and is useful for administrative tasks.

**Independent Test**: Can be fully tested by navigating to the owners list page and verifying that all existing owners are displayed.

**Acceptance Scenarios**:

1. **Given** there are multiple owners registered in the system, **When** a user navigates to the "Owners" list page, **Then** all registered owners are displayed, showing at least their name and city.

---

### User Story 4 - Update Existing Owner (Priority: P2)

**Description**: As a clinic staff member, I want to update an existing owner's information so that I can keep their contact details accurate.

**Why this priority**: Ensures data integrity and allows for corrections to owner information.

**Independent Test**: Can be fully tested by selecting an owner, modifying their details, and verifying the changes are saved.

**Acceptance Scenarios**:

1. **Given** an existing owner is displayed on their details page, **When** the user clicks "Edit Owner", modifies the address, and saves the changes, **Then** the owner's address is updated on their details page.

---

### User Story 5 - Create a New Pet for an Owner (Priority: P3)

**Description**: As a clinic staff member, I want to add a new pet to an existing owner's record so that I can track their animals.

**Why this priority**: Essential for managing pet-specific information and services.

**Independent Test**: Can be fully tested by selecting an owner, navigating to their pet list, and adding a new pet with valid details.

**Acceptance Scenarios**:

1. **Given** an owner has no pets listed, **When** the user navigates to the owner's details page, clicks "Add New Pet", enters a pet name, birth date, and selects a pet type, and submits the form, **Then** the new pet is added to the owner's record and displayed in their pet list.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error displayed to the user.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error displayed to the user.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error displayed to the user.
- **Blank Address**: Owner creation/update with a blank address → validation error displayed to the user.
- **Blank City**: Owner creation/update with a blank city → validation error displayed to the user.
- **Non-existent Owner for Edit**: Attempting to edit an owner with an ID that does not exist → `IllegalArgumentException` indicating owner not found, and an appropriate error message shown to the user.
- **Non-existent Owner for Pet Creation**: Attempting to create a pet for an owner with an ID that does not exist → `IllegalArgumentException` indicating owner not found, and an appropriate error message shown to the user.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error displayed to the user.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error displayed to the user.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → validation error displayed to the user.
- **Duplicate Pet Name for Same Owner**: Attempting to save a pet with a name that already exists for the same owner → validation error displayed to the user.
- **Owner Not Found During Find**: Searching for owners with a last name that yields no results → displays "not found" error message to the user.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new pets for an owner.
- **FR-002**: System MUST allow updating an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow owners to be searched by last name.
- **FR-005**: System SHOULD display a list of pets associated with an owner.
- **FR-006**: System MUST allow owners to be created with address, city, and telephone number.
- **FR-007**: System MUST validate that owner's first name is not blank.
- **FR-008**: System MUST validate that owner's last name is not blank.
- **FR-009**: System MUST validate that owner's address is not blank.
- **FR-010**: System MUST validate that owner's city is not blank.
- **FR-011**: System MUST validate that owner's telephone number is exactly 10 digits.
- **FR-012**: System MUST allow updating an existing owner's information.
- **FR-013**: System MUST display a list of all owners.
- **FR-014**: System MUST allow searching for owners by last name prefix.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Includes address, city, telephone, and a list of associated pets.
- **Pet**: Represents a pet. Includes birth date, type, and a collection of visits.
- **PetType**: Represents the type of a pet (e.g., cat, dog).
- **Visit**: Represents a visit to the clinic for a pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 3 seconds.
- **SC-002**: New owner creation and redirection to details page completes within 5 seconds.
- **SC-003**: The list of all owners loads within 5 seconds.
- **SC-004**: 95% of users successfully create a new owner without encountering validation errors on the first attempt.
- **SC-005**: All mandatory fields for owner and pet creation are clearly indicated and validated.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed by clinic staff and potentially new clients.
- Standard web browser compatibility is assumed.
- Data retention policies for owner and pet information are handled by a separate system or are outside the scope of this feature.
- The "Person" entity is a base for "Owner" and its fields (first name, last name) are managed as part of the owner creation/update process.
- The telephone number format validation (`\d{10}`) is sufficient for current needs.
- The "BaseEntity" and "NamedEntity" provide necessary ID and name fields for core entities.