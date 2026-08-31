# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `007-owners-spring-petclinic`

**Created**: 2026-03-19

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly find their information.

**Why this priority**: This is a core functionality for managing owners and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list of owners.

**Acceptance Scenarios**:

1. **Given** there are owners in the system with last names "Smith", "Smythe", and "Jones", **When** a user searches for owners with the last name prefix "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** there are no owners with the last name "Davis", **When** a user searches for owners with the last name prefix "Dav", **Then** a "No owners found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a clinic staff member, I want to create a new owner profile so that I can register new clients.

**Why this priority**: Essential for onboarding new customers and expanding the client base.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner is created and their details page is displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields filled, **Then** the owner is created and redirected to the owner's details page.
2. **Given** a user is on the new owner form, **When** they submit the form with a blank address, **Then** a validation error is shown for the address field, and the owner is not created.

---

### User Story 3 - View Owner List (Priority: P2)

As a clinic staff member, I want to view a list of all owners so that I can get an overview of registered clients.

**Why this priority**: Provides a general overview and is useful for administrative tasks.

**Independent Test**: Can be fully tested by navigating to the owner list page and verifying that all existing owners are displayed.

**Acceptance Scenarios**:

1. **Given** there are multiple owners registered in the system, **When** a user navigates to the owners list page, **Then** all registered owners are displayed in a list.

---

### User Story 4 - Add a Pet to an Owner (Priority: P2)

As a clinic staff member, I want to add a new pet to an existing owner's profile so that I can track their animals.

**Why this priority**: Crucial for managing pet-specific information and services.

**Independent Test**: Can be fully tested by selecting an owner, navigating to their pet management section, and adding a new pet with valid details.

**Acceptance Scenarios**:

1. **Given** an owner exists in the system, **When** a user adds a new pet to that owner's profile with valid information, **Then** the pet is successfully associated with the owner.
2. **Given** an owner exists, **When** a user attempts to add a pet with a blank name, **Then** a validation error is shown for the pet's name, and the pet is not added.

---

### User Story 5 - Add a Visit for a Pet (Priority: P3)

As a clinic staff member, I want to add a visit record for a pet so that I can log medical history.

**Why this priority**: Important for maintaining a complete medical history for each pet.

**Independent Test**: Can be fully tested by selecting a pet, navigating to its visit history, and adding a new visit with valid details.

**Acceptance Scenarios**:

1. **Given** a pet exists for an owner, **When** a user adds a new visit for that pet with a valid date and description, **Then** the visit is successfully recorded for the pet.
2. **Given** a pet exists, **When** a user attempts to add a visit with a date in the past, **Then** a validation error is shown for the visit date, and the visit is not recorded.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address will result in a validation error.
- **Blank City**: Owner creation/update with a blank city will result in a validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern will result in a validation error.
- **Non-existent Owner ID**: Attempting to edit or access an owner with an ID that does not exist will throw an `IllegalArgumentException`.
- **Blank Pet Name**: Pet creation/update with a blank name will result in a validation error.
- **Missing Pet Type**: Pet creation with a missing pet type will result in a validation error.
- **Duplicate Pet Name**: Attempting to create a pet with a name that already exists for the same owner will result in a validation error.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date will result in a validation error.
- **Invalid Visit Date**: Visit creation with a date that is not in the future will result in a validation error.
- **Non-existent Owner ID for Visit**: Attempting to add a visit for a pet belonging to a non-existent owner will throw an `IllegalArgumentException`.
- **Non-existent Pet ID for Visit**: Attempting to add a visit for a pet that does not exist for a given owner will throw an `IllegalArgumentException`.
- **Owner Not Found during Find**: Searching for owners with a last name that yields no results will add a "notFound" validation error to the owner's lastName field.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new pets for an owner.
- **FR-002**: System MUST allow updating an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow finding owners by their last name.
- **FR-005**: System SHOULD allow adding new visits for a pet.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner with contact details and associated pets. Attributes include first name, last name, address, city, and telephone.
- **Pet**: Represents an animal belonging to an owner. Attributes include name, birth date, and type. Associated with an Owner and has multiple Visits.
- **PetType**: Represents the species of a pet (e.g., Cat, Dog).
- **Visit**: Represents a medical visit for a pet. Attributes include date and description. Associated with a Pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 3 seconds.
- **SC-002**: New owner creation and redirection to their details page completes in under 5 seconds.
- **SC-003**: The owner list page loads displaying all owners within 4 seconds.
- **SC-004**: Adding a new pet to an owner's profile is confirmed within 3 seconds.
- **SC-005**: Adding a visit for a pet is recorded and displayed within 3 seconds.
- **SC-006**: 95% of owner and pet data entry operations complete without validation errors due to correct input.

## Assumptions

- Users performing these actions are authenticated clinic staff members.
- The system has a mechanism for generating unique owner and pet IDs.
- The `spring-petclinic` application is running and accessible.
- Data persistence (e.g., database) is handled by the underlying framework.
- Standard date and time formats are used for input and display.