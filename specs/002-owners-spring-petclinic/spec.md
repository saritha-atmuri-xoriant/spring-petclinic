# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-04

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly access their details and manage their pets.

**Why this priority**: This is a core functionality for managing pet owners and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a known owner's last name in the search field and verifying that their details are displayed. Delivers immediate value for staff looking up existing clients.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists, **When** a user searches for owners with the last name "Franklin", **Then** the system redirects to the owner's details page.
2. **Given** multiple owners whose last names start with "Smith" exist, **When** a user searches for owners with the last name "Smith", **Then** a list of owners matching the criteria is displayed.
3. **Given** no specific last name is provided in the search, **When** a user initiates a search, **Then** all owners are displayed.

---

### User Story 2 - Add New Owner (Priority: P2)

As a clinic staff member, I want to add a new owner to the system so that I can register new clients and their pets.

**Why this priority**: Essential for onboarding new customers to the clinic.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner is added to the system and searchable.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and submit the form, **Then** the new owner is created and displayed in the owner list.
2. **Given** the user is on the "Add Owner" page, **When** they leave the address field blank and submit the form, **Then** a validation error is shown for the address field, and the owner is not created.

---

### User Story 3 - Edit Existing Owner (Priority: P3)

As a clinic staff member, I want to edit the details of an existing owner so that I can keep their information up-to-date.

**Why this priority**: Important for maintaining accurate client records.

**Independent Test**: Can be fully tested by selecting an owner, modifying their details, and verifying the changes are saved and reflected.

**Acceptance Scenarios**:

1. **Given** an existing owner is selected, **When** the user modifies their telephone number and submits the form, **Then** the owner's telephone number is updated.
2. **Given** an existing owner is selected, **When** the user attempts to change the city to a blank value and submits the form, **Then** a validation error is shown for the city field, and the owner's details are not updated.

---

### Edge Cases

- What happens when an owner is created or updated with a telephone number that is not exactly 10 digits? → Validation error.
- How does the system handle an attempt to find or edit an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when a user searches for owners by last name and no results are found? → A "not found" message is displayed.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner with first name, last name, address, city, and telephone.
- **FR-002**: System MUST allow the updating of an existing owner's details (address, city, telephone).
- **FR-003**: System MUST validate that the owner's first name is not blank.
- **FR-004**: System MUST validate that the owner's last name is not blank.
- **FR-005**: System MUST validate that the owner's address is not blank.
- **FR-006**: System MUST validate that the owner's city is not blank.
- **FR-007**: System MUST validate that the owner's telephone number consists of exactly 10 digits.
- **FR-008**: System MUST allow searching for owners by last name.
- **FR-009**: System MUST display all owners when no last name is provided for search.
- **FR-010**: System MUST handle cases where an owner is not found when attempting to edit their details.
- **FR-011**: System MUST display a "not found" message when a last name search yields no results.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include address, city, and telephone. Has a one-to-many relationship with Pets.
- **Pet**: Represents a pet belonging to an owner. Key attributes include birthDate and type. Has a many-to-one relationship with PetType and a one-to-many relationship with Visits.
- **PetType**: Represents the type of a pet (e.g., cat, dog). Key attribute is its name.
- **Visit**: Represents a visit to the clinic for a pet. Key attribute is the date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find an owner by last name in under 3 seconds.
- **SC-002**: New owners can be successfully added and their details validated within 1 minute of form submission.
- **SC-003**: 95% of owner searches by last name return accurate results or a clear "not found" message.
- **SC-004**: Owner record updates are reflected immediately upon saving.

## Assumptions

- Users performing these actions are clinic staff with appropriate permissions.
- The system has a pre-populated list of pet types.
- The system has existing owner data for testing search functionality.
- The telephone number format `\d{10}` is sufficient for all required regions.