# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `017-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given owners exist in the system, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for basic operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list of owners. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for owners with the last name prefix "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** there are no owners with the last name "Davis", **When** the user searches for owners with the last name prefix "Dav", **Then** a "No owners found" message is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's list.

**Why this priority**: This is a fundamental operation for adding new customers to the clinic.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and confirming the owner appears in the owner list. Delivers the ability to onboard new clients.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Save", **Then** the new owner is added to the system and the user is redirected to the "Owners List" page, displaying the newly added owner.

---

### User Story 3 - View Owner Details (Priority: P2)

Given an owner exists, When the user navigates to the owner's details page, Then all owner attributes are displayed.

**Why this priority**: Allows users to view comprehensive information about a specific owner, which is crucial for managing their pets and visits.

**Independent Test**: Can be fully tested by selecting an owner from the list and verifying all their details are presented correctly. Delivers the ability to access detailed owner information.

**Acceptance Scenarios**:

1. **Given** an owner named "John Doe" exists with address "123 Main St", city "Anytown", and telephone "1234567890", **When** the user clicks on "John Doe" from the owners list, **Then** the owner details page is displayed showing "John Doe", "123 Main St", "Anytown", and "1234567890".

---

### User Story 4 - Add a New Pet for an Existing Owner (Priority: P2)

Given an existing owner, When the user navigates to the owner's details page and initiates adding a new pet, Then they can provide pet details and save the new pet associated with that owner.

**Why this priority**: Essential for managing the pets belonging to an owner.

**Independent Test**: Can be fully tested by selecting an owner, adding a new pet with valid details, and confirming the pet is listed under that owner. Delivers the ability to register new pets.

**Acceptance Scenarios**:

1. **Given** owner "Jane Smith" exists, **When** the user navigates to Jane Smith's details page, clicks "Add New Pet", fills in the pet's name, birth date, and selects a pet type, and clicks "Save", **Then** the new pet is associated with Jane Smith and appears in her pet list.

---

### User Story 5 - Update an Existing Pet's Information (Priority: P3)

Given a pet exists for an owner, When the user navigates to the pet's details and initiates an update, Then they can modify and save changes to the pet's information.

**Why this priority**: Allows for correction or modification of pet details as needed.

**Independent Test**: Can be fully tested by selecting a pet, changing a detail like its name, and confirming the update. Delivers the ability to maintain accurate pet records.

**Acceptance Scenarios**:

1. **Given** pet "Buddy" owned by "John Doe" exists, **When** the user navigates to Buddy's details, changes the pet's name to "Buddy Jr." and clicks "Save", **Then** the pet's name is updated to "Buddy Jr." in the system.

---

### Edge Cases

- What happens when an owner is created/updated with a blank address? → System rejects with validation error.
- What happens when an owner is created/updated with a blank city? → System rejects with validation error.
- What happens when an owner is created/updated with a telephone number not matching the `\d{10}` pattern? → System rejects with validation error.
- What happens when an owner search is performed with a blank last name? → System performs a broad search.
- What happens when attempting to edit an owner with an ID that does not exist? → System throws `IllegalArgumentException`.
- What happens when an owner search returns no results? → System displays a "not found" error message.
- What happens when a pet is created/updated with a blank name? → System rejects with "required" validation error.
- What happens when a pet is created/updated without selecting a pet type? → System rejects with "required" validation error.
- What happens when attempting to add a pet with a name that already exists for the same owner? → System rejects with "duplicate" validation error.
- What happens when a pet is created/updated with a birth date in an incorrect format (e.g., "2015/02/12")? → System rejects with "typeMismatch" validation error.
- What happens when `PetValidator` flags a pet with a blank name as an error? → Validation error is raised.
- What happens when `PetValidator` flags a pet with a null type as an error? → Validation error is raised.
- What happens when `PetValidator` flags a pet with a null birth date as an error? → Validation error is raised.
- What happens when a visit is created with a date that is not after the current date? → System rejects with "typeMismatch.visitDate" validation error.
- What happens when attempting to add a visit for a pet that does not exist for a given owner? → System throws `IllegalArgumentException`.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow finding owners by their last name.
- **FR-005**: System SHOULD allow adding a new visit for a pet.
- **FR-006**: System MUST allow the creation of a new owner.
- **FR-007**: System MUST allow the viewing of an owner's details.
- **FR-008**: System MUST allow the updating of an owner's information.
- **FR-009**: System MUST enforce validation rules for owner fields (first name, last name, address, city, telephone).
- **FR-010**: System MUST enforce validation rules for pet fields (name, birth date, type).
- **FR-011**: System MUST enforce validation rules for visit fields (date, description).

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Key attributes include first name, last name, address, city, and telephone number. An owner can have multiple pets.
- **Pet**: Represents a pet belonging to an owner. Key attributes include name, birth date, and type. A pet can have multiple visits.
- **PetType**: Represents the type of pet (e.g., Dog, Cat). Key attributes include name.
- **Visit**: Represents a visit to the clinic for a pet. Key attributes include date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully create a new owner in under 1 minute.
- **SC-002**: Users can find owners by last name prefix in under 5 seconds.
- **SC-003**: 95% of pet creation/update operations complete successfully with valid data.
- **SC-004**: All owner and pet validation errors are clearly communicated to the user.
- **SC-005**: The system supports at least 100 concurrent users browsing owner lists without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing authentication mechanisms.
- Data for owners, pets, and visits will be persisted in a relational database.
- The application will be deployed in an environment where standard web protocols are available.
- The "owners" module is a core part of the Spring Petclinic application and will be accessible via standard web interfaces.