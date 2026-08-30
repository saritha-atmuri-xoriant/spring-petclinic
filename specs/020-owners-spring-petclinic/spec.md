# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `020-owners-spring-petclinic`

**Created**: 2026-08-29

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's detail page.

**Why this priority**: This is a core functionality for managing pet owners and is essential for users to locate and view specific owner information.

**Independent Test**: Can be fully tested by entering "Franklin" in the last name search field and verifying redirection to the correct owner's detail page.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists in the system, **When** a user navigates to the "Find Owners" page and enters "Franklin" in the "Last name" field, **Then** the system redirects the user to the detail page for the owner named "Franklin".

---

### User Story 2 - Find Owners with Partial Last Name Match (Priority: P2)

Given multiple owners whose last names start with "Frank" exist, When a user searches for owners with the last name "Frank", Then a list of owners whose last names start with "Frank" is displayed.

**Why this priority**: This allows for more flexible searching and is a common user expectation when dealing with potentially incomplete information.

**Independent Test**: Can be fully tested by entering "Frank" in the last name search field and verifying that all owners whose last names begin with "Frank" are displayed in a list.

**Acceptance Scenarios**:

1. **Given** multiple owners exist with last names such as "Franklin", "Frankenstein", and "Frank", **When** a user navigates to the "Find Owners" page and enters "Frank" in the "Last name" field, **Then** a list displaying owners with last names "Franklin", "Frankenstein", and "Frank" is shown.

---

### User Story 3 - Handle Empty Last Name Search (Priority: P3)

Given multiple owners exist, When a user searches for owners with an empty last name, Then all owners are displayed.

**Why this priority**: This provides a way to view all registered owners, which can be useful for administrative purposes or for users who want a comprehensive overview.

**Independent Test**: Can be fully tested by leaving the last name search field empty and verifying that all owners in the system are displayed.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** a user navigates to the "Find Owners" page and leaves the "Last name" field empty, **Then** a list of all owners in the system is displayed.

---

### User Story 4 - Create New Owner (Priority: P1)

Given a user is on the "Add Owner" page, When they fill in all required owner details (first name, last name, address, city, telephone) and submit the form, Then a new owner is successfully created and added to the system.

**Why this priority**: The ability to add new owners is fundamental to managing the pet clinic's client base.

**Independent Test**: Can be fully tested by filling out the "Add Owner" form with valid data and verifying the new owner appears in search results and on their detail page.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" page, **When** they enter valid data for first name ("John"), last name ("Doe"), address ("123 Main St"), city ("Anytown"), and telephone ("1234567890"), and submit the form, **Then** the new owner "John Doe" is created and visible in the system.

---

### User Story 5 - Update Existing Owner (Priority: P2)

Given a user is viewing an existing owner's detail page, When they choose to edit the owner's information, fill in updated details, and submit the form, Then the owner's information is successfully updated.

**Why this priority**: Allows for correction of errors or updating of owner details as circumstances change.

**Independent Test**: Can be fully tested by editing an existing owner's details and verifying the changes are reflected on their detail page and in search results.

**Acceptance Scenarios**:

1. **Given** an existing owner "John Doe" with address "123 Main St", **When** a user navigates to "John Doe's" detail page, clicks "Edit Owner", changes the address to "456 Oak Ave", and submits the form, **Then** the owner's address is updated to "456 Oak Ave".

---

### User Story 6 - Add Pet to Existing Owner (Priority: P1)

Given a user is viewing an owner's detail page, When they choose to add a new pet, fill in the pet's details (name, birth date, type), and submit the form, Then the new pet is successfully associated with the owner.

**Why this priority**: Core functionality for managing a pet owner's pets within the clinic system.

**Independent Test**: Can be fully tested by adding a pet to an owner and verifying the pet appears on the owner's detail page.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" exists, **When** a user navigates to "John Doe's" detail page, clicks "Add New Pet", enters pet name "Buddy", selects "Dog" as type, and provides a birth date, **Then** the pet "Buddy" is listed under "John Doe's" pets.

---

### User Story 7 - Update Existing Pet (Priority: P2)

Given a user is viewing an owner's detail page with associated pets, When they choose to edit a specific pet, update its details (name, birth date, type), and submit the form, Then the pet's information is successfully updated.

**Why this priority**: Allows for correction or updating of pet information.

**Independent Test**: Can be fully tested by editing a pet's details and verifying the changes are reflected on the owner's detail page.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" has a pet named "Buddy" of type "Dog", **When** a user navigates to "John Doe's" detail page, clicks to edit "Buddy", changes the pet type to "Golden Retriever", and submits the form, **Then** the pet's type is updated to "Golden Retriever".

---

### User Story 8 - Add Visit to Existing Pet (Priority: P1)

Given a user is viewing a pet's detail page, When they choose to add a new visit, fill in the visit details (date, description), and submit the form, Then the new visit is successfully associated with the pet.

**Why this priority**: Essential for tracking a pet's medical history and clinic interactions.

**Independent Test**: Can be fully tested by adding a visit to a pet and verifying the visit appears on the pet's detail page.

**Acceptance Scenarios**:

1. **Given** a pet "Buddy" exists for owner "John Doe", **When** a user navigates to "Buddy's" detail page, clicks "Add New Visit", enters a visit date and description "Routine check-up", and submits the form, **Then** the visit "Routine check-up" is listed under "Buddy's" visits.

---

### User Story 9 - Handle Invalid Owner Input (Priority: P2)

Given a user is attempting to create or update an owner, When they provide invalid data (e.g., blank address, invalid telephone format), Then the system displays appropriate validation errors and prevents the submission.

**Why this priority**: Ensures data integrity and guides users to provide correct information.

**Independent Test**: Can be fully tested by attempting to submit owner forms with invalid data and verifying error messages are displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Owner" page, **When** they leave the "Address" field blank and attempt to submit, **Then** a validation error message indicating "Address must not be blank" is displayed.
2. **Given** a user is on the "Add Owner" page, **When** they enter "123" for the "Telephone" field and attempt to submit, **Then** a validation error message indicating "Telephone must be 10 digits" is displayed.

---

### User Story 10 - Handle Invalid Pet Input (Priority: P2)

Given a user is attempting to create or update a pet, When they provide invalid data (e.g., blank name, missing type), Then the system displays appropriate validation errors and prevents the submission.

**Why this priority**: Ensures data integrity for pet records.

**Independent Test**: Can be fully tested by attempting to submit pet forms with invalid data and verifying error messages are displayed.

**Acceptance Scenarios**:

1. **Given** a user is on the "Add Pet" form for an owner, **When** they leave the "Name" field blank and attempt to submit, **Then** a validation error message indicating "Pet name must not be blank" is displayed.
2. **Given** a user is on the "Add Pet" form for an owner, **When** they do not select a "Type" for the pet and attempt to submit, **Then** a validation error message indicating "Pet type must be selected" is displayed.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → validation error.
- **Non-existent Owner ID**: Attempting to access or modify an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error.
- **Invalid Pet Birth Date Format**: Pet creation/update with a birth date that does not match the expected format → validation error.
- **Blank Pet Name Validation**: `PetValidator` flags a blank pet name as an error.
- **Null Pet Type Validation**: `PetValidator` flags a null pet type as an error.
- **Null Pet Birth Date Validation**: `PetValidator` flags a null birth date as an error.
- **Duplicate Pet Name for Same Owner**: Attempting to save a pet with a name that already exists for the same owner → validation error.
- **Invalid Visit Date**: Visit date is not after the current date → validation error.
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` is thrown.
- **Owner Not Found for Visit**: Attempting to add a visit for an owner ID that does not exist → `IllegalArgumentException` is thrown.
- **Exception Trigger**: Accessing the "/oups" endpoint → a `RuntimeException` is thrown, showcasing exception handling.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details (address, city, telephone).
- **FR-003**: System MUST allow finding owners by last name.
- **FR-004**: System MUST allow finding owners by partial last name match.
- **FR-005**: System MUST display all owners when the last name search is empty.
- **FR-006**: System MUST allow the creation of a new pet for an existing owner.
- **FR-007**: System MUST allow the update of an existing pet's details (name, birth date, type).
- **FR-008**: System SHOULD validate pet information during creation or update.
- **FR-009**: System MUST allow the creation of a new visit for an existing pet.
- **FR-010**: System MUST validate owner input fields (address, city, telephone) for non-blank values and correct telephone format.
- **FR-011**: System MUST validate pet input fields (name, type) for non-blank values and correct format.
- **FR-012**: System MUST handle non-existent owner IDs gracefully by throwing an `IllegalArgumentException`.
- **FR-013**: System MUST handle non-existent pet IDs for an owner gracefully by throwing an `IllegalArgumentException`.
- **FR-014**: System MUST handle non-existent owner IDs when adding a visit gracefully by throwing an `IllegalArgumentException`.
- **FR-015**: System MUST trigger a `RuntimeException` when accessing the "/oups" endpoint to demonstrate exception handling.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner.
    - Attributes: address, city, telephone.
    - Relationships: Has multiple pets.
- **Pet**: Represents a pet.
    - Attributes: name, birthDate.
    - Relationships: Belongs to an owner, has multiple visits, has a type.
- **PetType**: Represents the type of a pet (e.g., dog, cat).
    - Attributes: name.
- **Visit**: Represents a visit to the clinic for a pet.
    - Attributes: date, description.
    - Relationships: Belongs to a pet.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully find owners by last name in under 3 seconds.
- **SC-002**: New owners can be created with all required fields in under 1 minute.
- **SC-003**: New pets can be added to an existing owner in under 1 minute.
- **SC-004**: Validation errors for owner and pet creation/updates are displayed clearly to the user within 1 second of submission.
- **SC-005**: 95% of owner and pet data entries meet the defined validation rules.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Standard date and time formats will be used for input.
- The underlying persistence layer (database) is functional and accessible.
- The project's existing `Person` and `NamedEntity` base classes will be utilized for owner and pet attributes respectively.
- The `PetType` entity will have a predefined set of types available for selection.
- The `Visit` entity will require a date and a description.
- The system will use standard Spring Boot validation mechanisms.
- The exception handling for non-existent IDs will follow the specified `IllegalArgumentException` pattern.
- The "/oups" endpoint is for demonstrating exception handling and not a core user-facing feature.