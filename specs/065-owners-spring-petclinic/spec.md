# Feature Specification: Owner Management

**Feature Branch**: `065-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for navigating the application and finding specific owner information, essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering "Franklin" in the last name field, and verifying redirection to the correct owner's details.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists in the system, **When** a user navigates to the owner search page and enters "Franklin" into the "Last Name" field, **Then** the system displays the details of the owner named "Franklin".
2. **Given** no owners with the last name "Smith" exist in the system, **When** a user navigates to the owner search page and enters "Smith" into the "Last Name" field, **Then** the system displays a "not found" message.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and a success message is displayed.

**Why this priority**: This is a fundamental operation for adding new clients to the clinic's system.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in all required fields with valid data, submitting the form, and verifying the owner is created and a success message is shown.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they enter valid data for first name, last name, address, city, telephone, and submit the form, **Then** a new owner record is created in the system, and the user is redirected to the owner's details page with a success indicator.
2. **Given** a user is on the "Add Owner" form, **When** they enter a valid first name, last name, address, city, and a 10-digit telephone number, **Then** the owner is successfully created.

---

### User Story 3 - Handle Invalid Owner Creation (Priority: P2)

Given a user is on the new owner form, When they submit an invalid owner form, Then the system displays an error message and returns to the form.

**Why this priority**: Ensures data integrity and provides user feedback for incorrect inputs.

**Independent Test**: Can be fully tested by navigating to the new owner form, entering invalid data in one or more fields, submitting the form, and verifying that error messages are displayed for the invalid fields and the form remains visible.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" form, **When** they leave the "First Name" field blank and submit the form, **Then** an error message indicating that the first name is required is displayed, and the form remains visible with the entered data preserved.
2. **Given** a user is on the "Add Owner" form, **When** they enter an invalid telephone number (e.g., "123") and submit the form, **Then** an error message indicating an invalid telephone format is displayed, and the form remains visible.
3. **Given** a user is on the "Add Owner" form, **When** they leave the "Address" field blank and submit the form, **Then** an error message indicating that the address is required is displayed, and the form remains visible.

---

### User Story 4 - Add a New Pet for an Existing Owner (Priority: P2)

Given an existing owner, When a user navigates to the owner's details page and initiates the process to add a new pet, Then they can provide pet details and associate it with the owner.

**Why this priority**: Allows for comprehensive pet management for each owner.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their details, initiating pet addition, filling in valid pet details, and verifying the pet is associated with the owner.

**Acceptance Scenarios**:

1. **Given** an existing owner "John Doe" exists, **When** a user navigates to "John Doe's" details page and selects the option to add a new pet, **Then** a form to add a new pet is displayed, allowing input for pet name, birth date, and type.
2. **Given** a user has filled out the new pet form with valid data (name, birth date, type) for owner "John Doe", **When** they submit the form, **Then** the new pet is successfully created and associated with "John Doe".

---

### User Story 5 - Add a New Visit for a Pet (Priority: P3)

Given an existing pet belonging to an owner, When a user navigates to the pet's details page and initiates the process to add a new visit, Then they can provide visit details and associate it with the pet.

**Why this priority**: Essential for tracking the medical history of pets.

**Independent Test**: Can be fully tested by selecting an existing pet, navigating to its details, initiating visit addition, filling in valid visit details, and verifying the visit is associated with the pet.

**Acceptance Scenarios**:

1. **Given** an existing pet "Buddy" belonging to owner "Jane Smith" exists, **When** a user navigates to "Buddy's" details page and selects the option to add a new visit, **Then** a form to add a new visit is displayed, allowing input for visit date and description.
2. **Given** a user has filled out the new visit form with valid data (date, description) for pet "Buddy", **When** they submit the form, **Then** the new visit is successfully created and associated with "Buddy".

---

### Edge Cases

- What happens when an owner is created/updated with a blank first name? → Validation error.
- What happens when an owner is created/updated with a blank last name? → Validation error.
- What happens when an owner is created/updated with a telephone number not matching the `\d{10}` pattern? → Validation error.
- What happens when an owner is created/updated with a blank address? → Validation error.
- What happens when an owner is created/updated with a blank city? → Validation error.
- What happens when attempting to edit an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when attempting to create a pet for an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when attempting to create a visit for a pet belonging to an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when attempting to create a visit for a pet with an ID that does not exist for a given owner? → `IllegalArgumentException` is thrown.
- What happens when a pet is created/updated with a blank name? → Validation error.
- What happens when a pet is created/updated without selecting a pet type? → Validation error.
- What happens when a pet is created/updated without providing a birth date? → Validation error.
- What happens when a pet is updated with a birth date in an incorrect format (e.g., "2015/02/12")? → `typeMismatch` validation error.
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error.
- What happens when a visit is created with a date that is not in the future? → `typeMismatch.visitDate` validation error.
- What happens when searching for owners with a last name that does not exist in the database? → `notFound` validation error on `lastName`.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the updating of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow finding owners by their last name.
- **FR-005**: System SHOULD allow adding a new visit for a pet.
- **FR-006**: System MUST allow the creation of new owner records.
- **FR-007**: System MUST validate owner information (first name, last name, address, city, telephone) during creation and update.
- **FR-008**: System MUST validate pet information (name, birth date, type) during creation and update.
- **FR-009**: System MUST validate visit information (date, description) during creation.
- **FR-010**: System MUST prevent a pet from having a duplicate name for the same owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their personal details (first name, last name, address, city, telephone) and a collection of associated pets.
- **Pet**: Represents a pet, including its name, birth date, type, and association with an owner.
- **PetType**: Represents the classification of a pet (e.g., Dog, Cat, Hamster).
- **Visit**: Represents a veterinary visit for a pet, including the date and a description of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully search for and view owner details within 5 seconds.
- **SC-002**: New owner records can be created with valid data in under 1 minute.
- **SC-003**: New pet records can be added to an existing owner in under 1 minute.
- **SC-004**: New visit records can be added to an existing pet in under 1 minute.
- **SC-005**: 99% of owner, pet, and visit creation/update operations complete successfully with valid data.
- **SC-006**: Validation errors are displayed clearly and accurately for all invalid inputs.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- Standard date and time formats will be used for input.
- The system will use a relational database for data persistence.
- The application will be deployed in a standard web server environment.
- The primary users are clinic staff responsible for managing owner and pet information.