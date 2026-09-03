# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `004-owners-spring-petclinic`

**Created**: 2026-09-03

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - View and Search Owners (Priority: P1)

As a clinic staff member, I want to be able to view a list of all owners and search for specific owners by their last name, so that I can quickly access owner information.

**Why this priority**: This is a core functionality for managing the clinic's customer base and is essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the owner's list page, entering a last name in the search field, and verifying the displayed results match the search criteria.

**Acceptance Scenarios**:

1. **Given** there are multiple owners in the system, **When** I navigate to the "Owners" page, **Then** I see a list of all owners displayed.
2. **Given** I am on the "Owners" page and there are owners with the last name "Franklin", **When** I search for "Franklin", **Then** the system displays only owners whose last name starts with "Franklin".
3. **Given** I am on the "Owners" page and search for a last name that yields no results, **When** I perform the search, **Then** a "Owner not found" message is displayed.
4. **Given** I am on the "Owners" page and search for an empty last name, **When** I perform the search, **Then** all owners are displayed, paginated.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a clinic staff member, I want to be able to create a new owner record, so that I can onboard new clients into the system.

**Why this priority**: Essential for expanding the clinic's client base and maintaining accurate records.

**Independent Test**: Can be fully tested by navigating to the "Add Owner" form, filling in all required valid fields, submitting the form, and verifying the new owner appears in the owner list and on their detail page.

**Acceptance Scenarios**:

1. **Given** I am on the "Add Owner" form, **When** I enter valid details for a new owner (first name, last name, address, city, telephone), **Then** the owner is successfully created and I am redirected to the owner's detail page.
2. **Given** I am on the "Add Owner" form, **When** I enter an invalid telephone number (e.g., not 10 digits), **Then** a validation error is displayed for the telephone field, and the form is re-rendered.
3. **Given** I am on the "Add Owner" form, **When** I leave the address or city field blank, **Then** validation errors are displayed for the respective fields, and the form is re-rendered.

---

### User Story 3 - Update an Existing Owner (Priority: P2)

As a clinic staff member, I want to be able to update the details of an existing owner, so that I can keep their information current.

**Why this priority**: Important for maintaining accurate client records and ensuring communication channels are up-to-date.

**Independent Test**: Can be fully tested by navigating to an existing owner's detail page, editing a field (e.g., address), saving the changes, and verifying the updated information is displayed.

**Acceptance Scenarios**:

1. **Given** I am viewing an owner's detail page, **When** I edit the owner's address and save, **Then** the address is updated and displayed correctly.
2. **Given** I am viewing an owner's detail page, **When** I attempt to update the owner's telephone number to an invalid format (e.g., 9 digits), **Then** a validation error is displayed for the telephone field, and the changes are not saved.
3. **Given** I am viewing an owner's detail page, **When** I attempt to update the owner's address to be blank, **Then** a validation error is displayed for the address field, and the changes are not saved.

---

### User Story 4 - Manage Pets for an Owner (Priority: P2)

As a clinic staff member, I want to be able to add new pets to an owner's record and update existing pet details, so that I can manage all aspects of a client's animal care.

**Why this priority**: Directly supports the core service offering of the clinic by managing pet information.

**Independent Test**: Can be fully tested by selecting an owner, navigating to their pet management section, adding a new pet with valid details, and verifying it appears. Then, editing an existing pet's name and saving to confirm the update.

**Acceptance Scenarios**:

1. **Given** I am viewing an owner's detail page, **When** I choose to add a new pet and provide valid pet details (name, birth date, type), **Then** the new pet is associated with the owner.
2. **Given** I am viewing an owner's detail page with existing pets, **When** I edit a pet's name and save, **Then** the pet's name is updated.
3. **Given** I am viewing an owner's detail page, **When** I attempt to add a pet with a blank name, **Then** a validation error is displayed for the pet's name.
4. **Given** I am viewing an owner's detail page, **When** I attempt to add a pet with a missing pet type, **Then** a validation error is displayed for the pet type.
5. **Given** I am viewing an owner's detail page, **When** I attempt to add a pet with a name that already exists for that owner, **Then** a validation error is displayed indicating a duplicate name.

---

### User Story 5 - Record Pet Visits (Priority: P3)

As a clinic staff member, I want to be able to record visits for a pet, so that a history of the pet's medical care is maintained.

**Why this priority**: Important for tracking pet health history, but secondary to core owner and pet management.

**Independent Test**: Can be fully tested by selecting a pet belonging to an owner, navigating to the visit recording section, adding a new visit with a valid date, and verifying it appears in the pet's visit history.

**Acceptance Scenarios**:

1. **Given** I am viewing a pet's detail page, **When** I add a new visit with a valid date, **Then** the visit is recorded and displayed in the pet's visit history.
2. **Given** I am viewing a pet's detail page, **When** I attempt to add a visit with a date that is not after the current date, **Then** a validation error is displayed for the visit date.

---

### Edge Cases

- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the 10-digit pattern → validation error.
- **Non-existent Owner ID**: Attempting to access or modify an owner with an ID that does not exist → `IllegalArgumentException` indicating owner not found.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error.
- **Missing Pet Type**: Pet creation with a missing pet type → validation error.
- **Duplicate Pet Name**: Attempting to create a pet with a name that already exists for the same owner → validation error indicating duplication.
- **Blank Pet Name on Update**: Pet update with a blank name → validation error.
- **Invalid Birth Date Format on Update**: Pet update with a birth date in an incorrect format → validation error `typeMismatch`.
- **Blank Pet Name Validation**: Pet validation with an empty name → `PetValidator` flags a field error for "name".
- **Null Pet Type Validation**: Pet validation with a null type → `PetValidator` flags a field error for "type".
- **Null Birth Date Validation**: Pet validation with a null birth date → `PetValidator` flags a field error for "birthDate".
- **Visit Date Not After Today**: Creating a visit with a date that is not after the current date → validation error `typeMismatch.visitDate`.
- **Non-existent Pet ID for Visit**: Attempting to create a visit for a pet that does not exist for a given owner → `IllegalArgumentException` indicating pet not found.
- **Owner Not Found for Visit**: Attempting to create a visit for an owner that does not exist → `IllegalArgumentException` indicating owner not found.
- **Find Owner with Empty Last Name**: Searching for owners with an empty last name → returns all owners paginated.
- **Find Owner with Non-existent Last Name**: Searching for owners with a last name that yields no results → validation error `notFound` for "lastName".
- **Owner Update with Blank Fields**: Updating an owner with blank address or telephone → validation errors for "address" and "telephone".

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow searching for owners by last name.
- **FR-003**: System MUST allow updating existing owner details (address, city, telephone).
- **FR-004**: System MUST allow the creation of new pets for an owner.
- **FR-005**: System MUST allow updating an existing pet's name.
- **FR-006**: System MUST allow recording visits for a pet.
- **FR-007**: System SHOULD validate owner information (address, city, telephone format) during creation and update.
- **FR-008**: System SHOULD validate pet information (name, birth date, type) during creation and update.
- **FR-009**: System SHOULD validate visit information (date) during creation.
- **FR-010**: System SHOULD provide a list of available pet types for selection when adding a pet.
- **FR-011**: System SHOULD handle potential data integrity violations during owner, pet, and visit operations.
- **FR-012**: System MUST display appropriate error messages for invalid input.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (name, address, city, telephone) and a collection of associated pets.
- **Pet**: Represents an animal owned by a person, including its name, birth date, type, and a history of visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a record of a pet's visit to the clinic, including the date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation and successful redirection to the owner's detail page completes in under 5 seconds.
- **SC-003**: 95% of users can successfully add a new pet to an owner's record without encountering validation errors on the first attempt.
- **SC-004**: System handles 100 concurrent requests for owner data retrieval without performance degradation.
- **SC-005**: All validation errors for owner, pet, and visit creation/updates are clearly displayed to the user.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing `Person` and `NamedEntity` base classes.
- The system will leverage Jakarta Bean Validation for input validation.
- The system will use standard JPA for persistence.
- The system will use standard Spring MVC for web interactions.
- Mobile support is out of scope for this iteration.
- The primary user for managing owners, pets, and visits is clinic staff.
- The telephone number format validation will strictly enforce 10 digits.
- The visit date validation will ensure the date is in the future or present.
- The system will display a generic "Owner not found" message for non-existent owner searches.
- The system will display a generic "Pet not found" or "Owner not found" message for invalid IDs in visit creation.
- The system will display a generic "Pet name already exists for this owner" message for duplicate pet names.
- The system will display a generic "Invalid telephone number format" message for telephone validation failures.
- The system will display a generic "Address cannot be blank" and "City cannot be blank" messages for owner address/city validation failures.
- The system will display a generic "Pet name cannot be blank" message for pet name validation failures.
- The system will display a generic "Pet type is required" message for missing pet type validation failures.
- The system will display a generic "Visit date must be after today" message for visit date validation failures.
- The system will display a generic "Invalid birth date format" message for pet birth date validation failures.