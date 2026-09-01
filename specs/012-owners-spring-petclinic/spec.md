# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `012-owners-spring-petclinic`

**Created**: 2026-03-19

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for managing pet clinic data, allowing staff to quickly access specific owner information.

**Independent Test**: Can be fully tested by searching for an existing owner's last name and verifying redirection to their detail page.

**Acceptance Scenarios**:

1. **Given** an owner named "John Franklin" exists, **When** a user searches for owners with the last name "Franklin", **Then** the system displays the details for John Franklin.

---

### User Story 2 - Find Owners with Partial Last Name Match (Priority: P2)

Given owners with last names starting with "Frank" exist, When a user searches for owners with the last name "Frank", Then a list of owners is displayed.

**Why this priority**: This provides flexibility for users who may not know the exact spelling or full last name, improving search usability.

**Independent Test**: Can be fully tested by searching for a partial last name and verifying that all matching owners are listed.

**Acceptance Scenarios**:

1. **Given** owners "John Franklin" and "Jane Franks" exist, **When** a user searches for owners with the last name "Frank", **Then** a list containing both "John Franklin" and "Jane Franks" is displayed.

---

### User Story 3 - Handle Empty Last Name Search (Priority: P3)

Given multiple owners exist, When a user searches for owners with an empty last name, Then all owners are displayed.

**Why this priority**: This allows for a comprehensive view of all registered owners, useful for administrative tasks or general browsing.

**Independent Test**: Can be fully tested by performing a search with an empty last name field and verifying that all existing owners are returned.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** a user searches for owners with an empty last name, **Then** all owners are displayed in the search results.

---

### User Story 4 - Create New Owner (Priority: P1)

Given a user is on the owner management page, When they choose to add a new owner and provide all required information, Then the new owner is successfully created and displayed in the owner list.

**Why this priority**: The ability to add new owners is fundamental to managing the pet clinic's client base.

**Independent Test**: Can be fully tested by creating a new owner with valid data and verifying their presence in the owner list.

**Acceptance Scenarios**:

1. **Given** the user is on the owner management page, **When** they fill out the new owner form with valid first name, last name, address, city, and telephone, **Then** the new owner is saved and appears in the list of owners.

---

### User Story 5 - Edit Existing Owner (Priority: P2)

Given a user is viewing an existing owner's details, When they choose to edit the owner's information and provide updated valid details, Then the owner's information is updated and displayed correctly.

**Why this priority**: Allows for correction of errors or updating of owner information as needed.

**Independent Test**: Can be fully tested by editing an existing owner's details and verifying the changes.

**Acceptance Scenarios**:

1. **Given** an existing owner "John Franklin" with address "123 Main St", **When** the user edits the owner and changes the address to "456 Oak Ave", **Then** the owner's details now show "456 Oak Ave".

---

### User Story 6 - Add New Pet to Owner (Priority: P1)

Given a user is viewing an owner's details, When they choose to add a new pet for that owner and provide valid pet information, Then the new pet is successfully associated with the owner and displayed.

**Why this priority**: Core functionality for managing a pet clinic, allowing owners to register their pets.

**Independent Test**: Can be fully tested by adding a pet to an existing owner and verifying its association.

**Acceptance Scenarios**:

1. **Given** owner "John Franklin" exists, **When** the user adds a new pet named "Buddy" of type "Dog" with birth date "2020-05-15" to John Franklin, **Then** "Buddy" is listed as a pet belonging to "John Franklin".

---

### User Story 7 - Edit Existing Pet (Priority: P2)

Given a user is viewing a pet's details, When they choose to edit the pet's information and provide updated valid details, Then the pet's information is updated and displayed correctly.

**Why this priority**: Allows for correction of pet details or updating information like birth date or name.

**Independent Test**: Can be fully tested by editing an existing pet's details and verifying the changes.

**Acceptance Scenarios**:

1. **Given** pet "Buddy" belonging to "John Franklin" has birth date "2020-05-15", **When** the user edits "Buddy" and changes the birth date to "2020-06-20", **Then** "Buddy"'s details now show the birth date "2020-06-20".

---

### User Story 8 - Add Visit for Pet (Priority: P1)

Given a user is viewing a pet's details, When they choose to add a new visit for that pet and provide valid visit information, Then the new visit is successfully associated with the pet and displayed.

**Why this priority**: Essential for tracking pet health history and appointments.

**Independent Test**: Can be fully tested by adding a visit to an existing pet and verifying its association.

**Acceptance Scenarios**:

1. **Given** pet "Buddy" exists, **When** the user adds a visit for "Buddy" on date "2026-03-20" with description "Annual check-up", **Then** "Annual check-up" is listed as a visit for "Buddy" on "2026-03-20".

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` thrown.
- **No Owners Found**: Searching for owners with a last name that yields no results → error message "not found" displayed.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error "required".
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error "required".
- **Invalid Pet Birth Date Format**: Pet creation/update with a birth date in an invalid format (e.g., "2015/02/12") → validation error "typeMismatch".
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error "duplicate".
- **Invalid Visit Date**: Visit creation with a date that is not in the future → validation error "typeMismatch.visitDate".
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet that does not exist for the specified owner → `IllegalArgumentException` thrown.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow updating an existing owner's information (first name, last name, address, city, telephone).
- **FR-003**: System MUST allow searching for owners by last name (exact match and partial match).
- **FR-004**: System MUST display all owners when a search for an empty last name is performed.
- **FR-005**: System MUST allow the creation of new pets for an owner.
- **FR-006**: System MUST allow updating an existing pet's name, birth date, and type.
- **FR-007**: System SHOULD validate pet information during creation or update.
- **FR-008**: System SHOULD display a form for creating or updating pet details.
- **FR-009**: System SHOULD populate a list of available pet types for selection during pet creation/update.
- **FR-010**: System MUST allow the creation of new visits for a pet.
- **FR-011**: System MUST allow updating an existing visit's date and description.
- **FR-012**: System SHOULD validate visit information during creation or update.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Attributes include first name, last name, address, city, and telephone number. Has a one-to-many relationship with `Pet`.
- **Pet**: Represents a pet. Attributes include name, birth date, and type. Has a many-to-one relationship with `Owner` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the type of pet (e.g., Cat, Dog). Attribute includes name.
- **Visit**: Represents a visit to the clinic for a pet. Attributes include date and description. Has a many-to-one relationship with `Pet`.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find an owner by last name in under 3 seconds.
- **SC-002**: The system successfully creates and displays new owners, pets, and visits with 100% accuracy.
- **SC-003**: 95% of pet and owner data updates are reflected immediately upon saving.
- **SC-004**: Validation errors for owner and pet data are displayed clearly to the user within 1 second of submission.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Existing authentication and authorization mechanisms will be leveraged if applicable to owner management.
- The list of pet types is predefined and managed separately.
- Data integrity for relationships (e.g., ensuring a pet belongs to a valid owner) is maintained by the system.