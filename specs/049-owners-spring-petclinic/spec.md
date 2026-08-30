# Feature Specification: Owner Management

**Feature Branch**: `049-owners-spring-petclinic`

**Created**: 2026-08-30

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information and manage their pets.

**Why this priority**: This is a core functionality for managing existing clients and is frequently used.

**Independent Test**: Can be fully tested by entering a known owner's last name into the search field and verifying the correct owner details are displayed.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists, **When** a user searches for owners with the last name "Franklin", **Then** the system redirects to the owner's details page for "Franklin".
2. **Given** multiple owners exist with the last name "Smith", **When** a user searches for owners with the last name "Smith", **Then** a list of all owners with the last name "Smith" is displayed.
3. **Given** no owners exist with the last name "NonExistent", **When** a user searches for owners with the last name "NonExistent", **Then** a message indicating "Owner not found" is displayed.

---

### User Story 2 - View a List of Owners (Priority: P2)

As a clinic staff member, I want to view a list of all owners so that I can get an overview of all clients.

**Why this priority**: Provides a general overview and is useful for browsing or when a specific owner is not known.

**Independent Test**: Can be fully tested by navigating to the owners list page and verifying that all existing owners are displayed.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** a user navigates to the owners list page, **Then** all owners are displayed, showing at least their first name, last name, and city.

---

### User Story 3 - Create a New Owner (Priority: P3)

As a new client, I want to be able to register as an owner so that I can add my pets to the clinic's system.

**Why this priority**: Essential for onboarding new clients and expanding the customer base.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner is created and their details page is shown.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields filled, **Then** the owner is created and the user is redirected to the owner's details page.

---

### User Story 4 - Add a New Pet for an Owner (Priority: P1)

As an owner, I want to add a new pet to my profile so that I can manage their health records and appointments.

**Why this priority**: Core functionality for pet owners to manage their animals within the clinic's system.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their pet management section, and successfully adding a new pet with valid details.

**Acceptance Scenarios**:

1. **Given** an owner exists, **When** the owner navigates to add a new pet and submits valid pet details (name, type, birth date), **Then** the new pet is associated with the owner and appears in their pet list.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → validation error.
- **Non-existent Owner ID**: Attempting to access or modify an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error.
- **Missing Pet Birth Date**: Pet creation/update without providing a birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Visit creation/update with a date that is not after the current date → validation error.
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet that does not exist for a given owner → `IllegalArgumentException` is thrown.
- **Owner Not Found During Find**: Searching for owners with a last name that yields no results → validation error indicating "not found".

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for a given owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow finding owners by their last name.
- **FR-005**: System SHOULD allow inserting a new owner into the system.
- **FR-006**: System MUST allow viewing a list of all owners.
- **FR-007**: System MUST allow viewing the details of a specific owner.
- **FR-008**: System MUST allow updating an owner's contact information (address, city, telephone).
- **FR-009**: System MUST allow adding a new visit for a specific pet.
- **FR-010**: System MUST allow viewing a list of visits for a specific pet.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents an individual or entity that owns one or more pets. Attributes include first name, last name, address, city, and telephone number.
- **Pet**: Represents an animal owned by an Owner. Attributes include name, birth date, and type.
- **PetType**: Represents the category of a pet (e.g., Dog, Cat, Bird).
- **Visit**: Represents a medical visit for a Pet. Attributes include date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find an owner by last name and view their details in under 5 seconds.
- **SC-002**: New owners can be successfully created and their details displayed within 10 seconds of form submission.
- **SC-003**: A new pet can be added to an existing owner's profile in under 15 seconds.
- **SC-004**: The system supports displaying a list of up to 100 owners with an average load time of under 3 seconds.
- **SC-005**: 95% of owner and pet data entries are validated successfully upon submission, with clear error messages for invalid data.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing authentication mechanisms if applicable (though not explicitly detailed in the prompt).
- Data retention policies for owner and pet information will follow industry best practices for veterinary clinics unless otherwise specified.
- The primary users of this feature are clinic staff.
- Mobile support is out of scope for this initial specification.
- The system will use a standard relational database for persistence.