# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `005-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given a list of owners exists, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list, delivering the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for "Sm", **Then** owners "Smith" and "Smythe" are displayed.
2. **Given** there are no owners with the last name "Davis", **When** the user searches for "Davis", **Then** a message indicating no owners were found is displayed.
3. **Given** there are multiple owners, **When** the user enters an empty search term, **Then** all owners are displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: This is fundamental for onboarding new clients into the pet clinic system.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and confirming redirection to the owner's detail page, delivering the ability to add new clients.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and submit the form, **Then** the new owner is saved and the user is redirected to the details page for that newly created owner.
2. **Given** the user is on the "Add Owner" page, **When** they attempt to submit the form with a blank required field (e.g., last name), **Then** an appropriate validation error message is displayed for that field, and the owner is not created.

---

### User Story 3 - View Owner Details (Priority: P2)

Given an owner exists, When the user navigates to the owner's details page, Then all owner attributes are displayed.

**Why this priority**: Essential for accessing and reviewing information about existing clients.

**Independent Test**: Can be fully tested by navigating to an owner's detail page and verifying all associated information is present, delivering the ability to view client details.

**Acceptance Scenarios**:

1. **Given** an owner named "John Doe" exists with address "123 Main St", city "Anytown", and telephone "1234567890", and has pets "Buddy" (dog) and "Whiskers" (cat), **When** the user navigates to John Doe's owner details page, **Then** the owner's first name ("John"), last name ("Doe"), address ("123 Main St"), city ("Anytown"), telephone ("1234567890"), and a list of their pets ("Buddy", "Whiskers") are displayed.

---

### User Story 4 - Update Existing Owner (Priority: P2)

Given an owner exists and the user is on the owner's edit page, When they update owner details and submit the form, Then the owner's information is updated and they are redirected to the owner's details page.

**Why this priority**: Allows for maintaining accurate and up-to-date client information.

**Independent Test**: Can be fully tested by editing an owner's details and confirming the changes are saved and reflected on their detail page, delivering the ability to modify client information.

**Acceptance Scenarios**:

1. **Given** an owner "Jane Smith" exists, **When** the user navigates to Jane Smith's edit page, changes her telephone number to "9876543210", and submits the form, **Then** the owner's telephone number is updated to "9876543210", and the user is redirected to Jane Smith's details page showing the updated information.

---

### User Story 5 - Create a New Pet for an Owner (Priority: P3)

Given an owner exists and the user is on the owner's pet creation form, When they submit a valid pet form, Then the pet is created and associated with the owner.

**Why this priority**: Enables adding new pets to an owner's record, a common clinic operation.

**Independent Test**: Can be fully tested by adding a new pet to an owner's record and verifying its appearance on the owner's detail page, delivering the ability to register new pets.

**Acceptance Scenarios**:

1. **Given** owner "Alice Wonderland" exists, **When** the user navigates to add a pet for Alice, fills in the pet's name "Cheshire Cat", selects "Cat" as the pet type, and submits the form, **Then** the "Cheshire Cat" is created and listed under Alice Wonderland's pets.

---

### User Story 6 - Update Existing Pet Information (Priority: P3)

Given a pet exists for an owner and the user is on the pet's edit page, When they update pet details and submit the form, Then the pet's information is updated.

**Why this priority**: Allows for correcting or updating details of existing pets.

**Independent Test**: Can be fully tested by editing a pet's details and confirming the changes are saved, delivering the ability to modify pet information.

**Acceptance Scenarios**:

1. **Given** pet "Buddy" (dog) exists for owner "John Doe", **When** the user navigates to Buddy's edit page, changes his birth date to "2020-05-15", and submits the form, **Then** Buddy's birth date is updated to "2020-05-15".

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or access an owner with an ID that does not exist → `IllegalArgumentException` thrown.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error "required".
- **Missing Pet Type**: Pet creation/update without specifying a pet type → validation error "required".
- **Invalid Pet Birth Date Format**: Pet creation/update with a birth date in an incorrect format (e.g., "2015/02/12") → validation error "typeMismatch".
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error "duplicate".
- **Blank Visit Date**: Visit creation/update with a blank date → validation error.
- **Visit Date in the Past**: Visit creation/update with a date that is not after the current date → validation error "typeMismatch.visitDate".
- **Non-existent Owner ID for Visit**: Attempting to create a visit for an owner ID that does not exist → `IllegalArgumentException` thrown.
- **Non-existent Pet ID for Visit**: Attempting to create a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` thrown.
- **Empty Search Term**: Finding owners with an empty last name → returns all owners.
- **No Owners Found**: Searching for owners with a last name that does not exist → validation error "notFound" on lastName.
- **Triggering Runtime Exception**: Accessing the "/oups" endpoint → throws a `RuntimeException` and displays an error page.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new pets for an owner.
- **FR-002**: System MUST allow the updating of existing pet information.
- **FR-003**: System SHOULD validate pet data during creation or update.
- **FR-004**: System SHOULD provide a list of available pet types for selection.
- **FR-005**: System SHOULD handle cases where an owner is not found during pet operations.
- **FR-006**: System MUST allow the creation of new owners.
- **FR-007**: System MUST allow the updating of existing owner information.
- **FR-008**: System MUST validate owner data during creation or update.
- **FR-009**: System MUST allow searching for owners by last name.
- **FR-010**: System MUST display owner details, including their associated pets.
- **FR-011**: System MUST allow the creation of new visits for a pet.
- **FR-012**: System MUST allow the updating of existing visit information.
- **FR-013**: System MUST validate visit data during creation or update.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (address, city, telephone) and a collection of their pets.
- **Pet**: Represents a pet, including its name, birth date, and type. It is associated with an owner and has a history of visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a veterinary visit for a pet, including the date of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 2 seconds.
- **SC-002**: New owners can be created and their details viewed within 3 minutes of form submission.
- **SC-003**: 95% of pet creation/update operations complete successfully with valid data.
- **SC-004**: The system supports up to 50 concurrent users managing owner and pet data without performance degradation.
- **SC-005**: Support tickets related to incorrect owner or pet information are reduced by 30% after feature implementation.

## Assumptions

- Users have stable internet connectivity.
- The system will be accessed via a web browser.
- Standard date and time formats will be used for user input.
- The project will reuse existing Person and BaseEntity/NamedEntity abstractions.
- Data validation will follow the Java Bean Validation (JSR 380) standard.
- Persistence will be handled by Spring Data JPA.
- The application will be deployed in an environment supporting Spring Boot conventions.
- The primary language for user interaction will be English.
- The telephone number format `\d{10}` is sufficient for all supported regions.
- The system will not handle international phone numbers or complex address formats beyond city and street.
- The "owners" module is a self-contained unit for managing pet owners and their pets.
- No specific security requirements beyond standard input validation are defined for this feature.
- The "visit" functionality is considered part of the "owners" module for the purpose of this specification, implying direct association with an owner's pets.