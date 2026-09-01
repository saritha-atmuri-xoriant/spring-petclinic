# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `004-owners-spring-petclinic`

**Created**: 2026-03-19

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly access their details and manage their pets.

**Why this priority**: This is a core functionality for managing customer information and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a known last name in the search field and verifying that the correct owner's details are displayed.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists in the system,
   **When** a user searches for owners with the last name "Franklin",
   **Then** the system redirects to the owner's details page for "Franklin".
2. **Given** multiple owners exist with the last name "Smith",
   **When** a user searches for owners with the last name "Smith",
   **Then** a list of all owners with the last name "Smith" is displayed.
3. **Given** no owner exists with the last name "NonExistent",
   **When** a user searches for owners with the last name "NonExistent",
   **Then** a validation error is displayed indicating "Owner not found" for the last name field.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a new user, I want to create a new owner profile so that I can register my pets with the clinic.

**Why this priority**: This is fundamental for onboarding new clients and expanding the clinic's customer base.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying that the owner is successfully created and appears in the owner list.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form,
   **When** they submit a valid owner form with all required fields (first name, last name, address, city, telephone),
   **Then** the owner is created and added to the system, and the user is redirected to the owner's details page.
2. **Given** a user is on the new owner form,
   **When** they submit the form with a blank address,
   **Then** a validation error is displayed for the address field.
3. **Given** a user is on the new owner form,
   **When** they submit the form with an invalid telephone number (not 10 digits),
   **Then** a validation error is displayed for the telephone field.

---

### User Story 3 - View a List of Owners (Priority: P2)

As a clinic staff member, I want to view a list of all registered owners so that I can get an overview of the clinic's clientele.

**Why this priority**: Provides a general overview and is useful for administrative tasks and quick reference.

**Independent Test**: Can be fully tested by navigating to the owners list page and verifying that all existing owners are displayed.

**Acceptance Scenarios**:

1. **Given** there are multiple owners in the system,
   **When** a user navigates to the owners list page,
   **Then** all owners are displayed, showing at least their first name, last name, and address.
2. **Given** there are no owners in the system,
   **When** a user navigates to the owners list page,
   **Then** a message indicating "No owners found" is displayed.

---

### User Story 4 - Create a New Pet for an Existing Owner (Priority: P2)

As a clinic staff member, I want to add a new pet to an existing owner's record so that I can manage all of their animals.

**Why this priority**: Essential for maintaining accurate pet records associated with owners.

**Independent Test**: Can be fully tested by selecting an owner, navigating to their pet management section, and adding a new pet with valid details.

**Acceptance Scenarios**:

1. **Given** an existing owner with pets,
   **When** a user navigates to the owner's details page and initiates adding a new pet,
   **Then** a form to add a new pet is displayed.
2. **Given** the new pet form is displayed for an owner,
   **When** a user submits the form with a valid pet name, birth date, and pet type,
   **Then** the new pet is successfully created and associated with the owner.
3. **Given** the new pet form is displayed for an owner,
   **When** a user submits the form with a blank pet name,
   **Then** a validation error is displayed for the pet name field.
4. **Given** the new pet form is displayed for an owner,
   **When** a user attempts to add a pet with a name that already exists for that owner,
   **Then** a validation error is displayed indicating the pet name is a duplicate for this owner.

---

### User Story 5 - Update an Existing Pet's Information (Priority: P3)

As a clinic staff member, I want to update an existing pet's information (like name or birth date) so that the records remain accurate.

**Why this priority**: Ensures data integrity for pet records.

**Independent Test**: Can be fully tested by selecting a pet, navigating to its edit form, making a change, and verifying the update.

**Acceptance Scenarios**:

1. **Given** an existing pet associated with an owner,
   **When** a user navigates to the pet's details and initiates an update,
   **Then** a form to edit the pet's information is displayed.
2. **Given** the pet edit form is displayed,
   **When** a user updates the pet's name and submits the form,
   **Then** the pet's name is successfully updated.
3. **Given** the pet edit form is displayed,
   **When** a user updates the pet's birth date and submits the form,
   **Then** the pet's birth date is successfully updated.
4. **Given** the pet edit form is displayed,
   **When** a user submits the form with a blank pet name,
   **Then** a validation error is displayed for the pet name field.

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → validation error.
- **Non-existent Owner ID**: Attempting to access or modify an owner with an ID that does not exist → `IllegalArgumentException` indicating owner not found.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation with a missing pet type → validation error.
- **Invalid Pet Birth Date**: Pet creation/update with a null birth date → validation error.
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Visit creation with a date that is not after the current date → validation error.
- **Non-existent Pet ID for Owner**: Attempting to create a visit for a pet that does not exist for a given owner → `IllegalArgumentException` indicating pet not found.
- **Owner Not Found during Find**: Searching for owners with a last name that yields no results → validation error "notFound" on the lastName field.
- **Triggering Generic Exception**: Navigating to the "/oups" endpoint → `RuntimeException` is thrown, showcasing exception handling.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow updating an existing pet's name.
- **FR-003**: System SHOULD validate pet data during creation or update.
- **FR-004**: System SHOULD display a form for creating or updating a pet.
- **FR-005**: System SHOULD allow finding owners by last name.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (address, city, telephone) and a collection of associated pets.
- **Pet**: Represents a pet, including its name, birth date, type, and a history of visits.
- **PetType**: Represents the classification of a pet (e.g., dog, cat).
- **Visit**: Represents a single visit to the clinic for a pet, including the date of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner profiles can be created with all required fields in under 2 minutes.
- **SC-003**: The system successfully displays all registered owners on the list page.
- **SC-004**: Adding a new pet to an owner's record is completed successfully 95% of the time.
- **SC-005**: Updating an existing pet's name or birth date is successful 98% of the time.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing Person and NamedEntity base classes for Owner and Pet respectively.
- Data validation rules for telephone numbers and dates will follow standard formats.
- The system will handle non-existent owner or pet IDs by returning appropriate error messages.
- The "owners" module is a core part of the Spring Petclinic application and will be integrated as such.
- The primary users of this module are clinic staff.
- The `/oups` endpoint is for demonstrating exception handling and is not a core user-facing feature for this module.