# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-09-03

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for navigating the application and finding existing owner information, essential for basic operations.

**Independent Test**: Can be fully tested by searching for a known owner's last name and verifying the correct owner details page is displayed.

**Acceptance Scenarios**:

1. **Given** an owner named "John Franklin" exists in the system, **When** a user searches for owners with the last name "Franklin", **Then** the system displays the details for John Franklin.
2. **Given** no owners with the last name "Davis" exist, **When** a user searches for owners with the last name "Davis", **Then** the system displays a "not found" message.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and a success message is displayed.

**Why this priority**: Core functionality for adding new customers to the clinic.

**Independent Test**: Can be fully tested by filling out the owner creation form with valid data and verifying the owner is added and a success confirmation is shown.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they enter valid details (first name, last name, address, city, telephone), **Then** the owner is successfully created and the user is redirected to the owner's details page or a confirmation page.
2. **Given** a user is on the "Add Owner" form, **When** they enter valid details and a valid pet, **Then** the owner and their pet are successfully created.

---

### User Story 3 - Update an Existing Owner (Priority: P2)

Given a user is viewing an owner's details, When they choose to edit the owner and submit valid updated information, Then the owner's details are updated.

**Why this priority**: Allows for correction of errors or changes in owner information.

**Independent Test**: Can be fully tested by editing an existing owner's details and verifying the changes are saved.

**Acceptance Scenarios**:

1. **Given** an existing owner "Jane Doe" is displayed, **When** the user edits the owner's telephone number to a new valid number and saves, **Then** the owner's details reflect the updated telephone number.
2. **Given** an existing owner "Jane Doe" is displayed, **When** the user edits the owner's address and city and saves, **Then** the owner's details reflect the updated address and city.

---

### User Story 4 - Create a New Pet for an Owner (Priority: P2)

Given a user is viewing an owner's details, When they choose to add a new pet and submit valid pet information, Then the pet is created and associated with the owner.

**Why this priority**: Essential for managing the pets associated with each owner.

**Independent Test**: Can be fully tested by navigating to an owner's details, adding a new pet with valid information, and verifying it appears in the owner's pet list.

**Acceptance Scenarios**:

1. **Given** an owner "John Smith" is displayed with no pets, **When** the user adds a new pet named "Buddy" with a birth date and type "Dog", **Then** "Buddy" appears in John Smith's list of pets.
2. **Given** an owner "John Smith" is displayed with existing pets, **When** the user adds a new pet named "Whiskers" with a birth date and type "Cat", **Then** "Whiskers" is added to John Smith's pet list.

---

### User Story 5 - Handle Invalid Owner Creation (Priority: P3)

Given a user is on the new owner form, When they submit an invalid owner form, Then the system displays an error message and returns to the owner creation form.

**Why this priority**: Ensures data integrity by preventing invalid data from being saved.

**Independent Test**: Can be fully tested by submitting the owner creation form with invalid data (e.g., blank fields, incorrect phone format) and verifying appropriate error messages are shown.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they submit the form with a blank first name, **Then** an error message is displayed indicating the first name is required, and the form remains open.
2. **Given** a user is on the "Add Owner" form, **When** they submit the form with a telephone number that is not 10 digits, **Then** an error message is displayed indicating an invalid telephone format, and the form remains open.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error "required".
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error "required".
- **Invalid Pet Birth Date Format**: Pet creation/update with a birth date in an incorrect format (e.g., "2015/02/12") → validation error "typeMismatch".
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error "duplicate".
- **Owner Not Found During Find**: Searching for an owner by last name that does not exist → validation error "notFound" on the `lastName` field.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the updating of an existing owner's details (address, city, telephone).
- **FR-003**: System MUST allow finding owners by their last name.
- **FR-004**: System MUST allow the creation of a new pet for a given owner.
- **FR-005**: System MUST validate owner information (first name, last name, address, city, telephone) during creation and update.
- **FR-006**: System MUST validate pet information (name, birth date, type) during creation and update.
- **FR-007**: System MUST prevent duplicate pet names for the same owner.
- **FR-008**: System MUST display appropriate error messages for invalid owner or pet data.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Attributes include first name, last name, address, city, and telephone number. Has a one-to-many relationship with `Pet`.
- **Pet**: Represents a pet belonging to an owner. Attributes include name, birth date, and type. Has a many-to-one relationship with `PetType` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog). Attributes include name.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find an owner by last name in under 3 seconds.
- **SC-002**: New owners can be created with valid data in under 1 minute.
- **SC-003**: New pets can be added to an existing owner in under 1 minute.
- **SC-004**: 95% of invalid owner creation attempts result in clear, actionable error messages displayed to the user.
- **SC-005**: The system successfully prevents duplicate pet names for the same owner.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- Standard date and time formats will be used for input.
- The system will use a relational database for data persistence.
- Error messages will be user-friendly and informative.
- The primary language for the application is English.
- The system will reuse existing `Person` and `NamedEntity` base classes for owner and pet attributes respectively.
- The `PetType` entity will be pre-populated with common pet types.
- The `Visit` entity is related to `Pet` but its management is out of scope for this specific feature.
- The `OwnerController` and `PetController` will handle the user interface and interaction logic.
- The `ClinicService` will be used for business logic and data access.
- Validation rules defined in the repository context will be enforced.