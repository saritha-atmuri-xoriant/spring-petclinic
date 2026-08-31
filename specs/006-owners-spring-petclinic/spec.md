# Feature Specification: Owner Management

**Feature Branch**: `006-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for managing pet owners, allowing users to quickly locate specific individuals.

**Independent Test**: Can be fully tested by entering "Franklin" in the last name search field and verifying navigation to the correct owner's detail page.

**Acceptance Scenarios**:

1. **Given** an owner named "John Franklin" exists, **When** the user searches for owners with the last name "Franklin", **Then** the system displays the details for "John Franklin".

---

### User Story 2 - Find Owners with Partial Last Name Match (Priority: P2)

Given multiple owners whose last names start with "Frank" exist, When a user searches for owners with the last name "Frank", Then a list of owners whose last names start with "Frank" is displayed.

**Why this priority**: This provides flexibility for users who may not know the exact spelling of a last name, improving search usability.

**Independent Test**: Can be fully tested by entering "Frank" in the last name search field and verifying that all owners whose last names begin with "Frank" are listed.

**Acceptance Scenarios**:

1. **Given** owners "John Franklin" and "Jane Frank" exist, **When** the user searches for owners with the last name "Frank", **Then** both "John Franklin" and "Jane Frank" are displayed in the search results.

---

### User Story 3 - Handle Empty Last Name Search (Priority: P3)

Given multiple owners exist, When a user searches for owners with an empty last name, Then all owners are displayed on the owners list page.

**Why this priority**: This ensures that users can retrieve a complete list of all owners when no specific search criteria are provided.

**Independent Test**: Can be fully tested by leaving the last name search field empty and verifying that all existing owners are displayed.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** the user performs a search with an empty last name field, **Then** all owners are displayed on the owners list page.

---

### User Story 4 - Create New Owner (Priority: P1)

Given a user wants to add a new pet owner, When the user provides all required owner details (first name, last name, address, city, telephone), Then a new owner record is successfully created and displayed in the owner list.

**Why this priority**: Core functionality for expanding the pet owner database.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying the owner appears in the list.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they enter valid details for "Jane Doe", "123 Main St", "Anytown", and "1234567890", **Then** Jane Doe is added to the owner list.

---

### User Story 5 - Update Existing Owner (Priority: P2)

Given an existing owner's record, When the user modifies and saves the owner's details (address, city, telephone), Then the owner's record is updated with the new information.

**Why this priority**: Allows for maintaining accurate owner information.

**Independent Test**: Can be fully tested by editing an existing owner's details and verifying the changes are saved and reflected.

**Acceptance Scenarios**:

1. **Given** an owner "John Smith" exists at "456 Oak Ave", "Otherville", **When** the user edits John Smith's address to "789 Pine Ln" and city to "Newville", **Then** John Smith's record shows the updated address and city.

---

### User Story 6 - Add New Pet to Existing Owner (Priority: P1)

Given an existing owner, When the user provides all required pet details (name, birth date, type) for a new pet, Then the new pet is successfully associated with the owner.

**Why this priority**: Essential for managing pets associated with owners.

**Independent Test**: Can be fully tested by selecting an owner, adding a new pet with valid details, and verifying the pet appears under that owner.

**Acceptance Scenarios**:

1. **Given** owner "Jane Doe" exists, **When** the user adds a new pet named "Buddy", born "2020-05-15", of type "Dog", **Then** "Buddy" is listed as one of Jane Doe's pets.

---

### User Story 7 - Add New Visit for a Pet (Priority: P1)

Given an existing pet, When the user provides all required visit details (date, description), Then a new visit record is successfully associated with the pet.

**Why this priority**: Crucial for tracking pet's medical history.

**Independent Test**: Can be fully tested by selecting a pet, adding a new visit with valid details, and verifying the visit appears in the pet's visit history.

**Acceptance Scenarios**:

1. **Given** pet "Buddy" (owned by Jane Doe) exists, **When** the user adds a visit for "Buddy" on "2026-09-01" with description "Annual check-up", **Then** the visit is recorded for "Buddy".

---

### Edge Cases

- What happens when an owner is created/updated with a blank first name? → Validation error.
- What happens when an owner is created/updated with a blank last name? → Validation error.
- What happens when an owner is created/updated with a telephone number not matching the `\d{10}` pattern? → Validation error.
- What happens when an owner is created/updated with a blank address? → Validation error.
- What happens when an owner is created/updated with a blank city? → Validation error.
- What happens when attempting to edit or view an owner with an ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when searching for owners with a last name that yields no results? → System displays a "not found" error message.
- What happens when creating or updating a pet with a blank name? → Validation error "required".
- What happens when creating a pet without selecting a pet type? → Validation error "required".
- What happens when creating or updating a pet with a birth date in an incorrect format (e.g., "2015/02/12")? → Validation error "typeMismatch".
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error "duplicate".
- What happens when booking a visit with a date that is not in the future? → Validation error "typeMismatch.visitDate".
- What happens when attempting to add a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` is thrown.
- What happens when multiple concurrent requests attempt to add a pet with the same name for the same owner? → Only one request should succeed, and the others should fail to prevent duplicates.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow finding owners by last name.
- **FR-005**: System SHOULD allow adding a new visit for a pet.
- **FR-006**: System MUST allow the creation of a new owner.
- **FR-007**: System MUST allow the update of an existing owner's address, city, and telephone.
- **FR-008**: System MUST validate owner information (first name, last name, address, city, telephone) during creation or update.
- **FR-009**: System MUST allow adding a new pet to an existing owner, including pet name, birth date, and type.
- **FR-010**: System MUST validate pet information (name, birth date, type) during creation or update.
- **FR-011**: System MUST allow adding a new visit to an existing pet, including date and description.
- **FR-012**: System MUST validate visit information (date, description) during creation or update.
- **FR-013**: System MUST disallow the `id` field when creating or updating an owner.
- **FR-014**: System MUST disallow the `id` field when creating or updating a pet.
- **FR-015**: System MUST disallow the `id` field when creating or updating a visit.
- **FR-016**: System MUST ensure a pet's name is unique for a given owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Includes fields for address, city, and telephone number, and is associated with a collection of `Pet` objects.
- **Pet**: Represents a pet. Includes fields for birth date, `PetType`, and is associated with a collection of `Visit` objects.
- **PetType**: Represents the type of a pet (e.g., cat, dog).
- **Visit**: Represents a visit to the clinic for a pet. Includes fields for date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 2 seconds.
- **SC-002**: New owner creation is completed within 3 seconds.
- **SC-003**: Adding a new pet to an owner is completed within 3 seconds.
- **SC-004**: Adding a new visit for a pet is completed within 3 seconds.
- **SC-005**: 95% of owner/pet/visit creation or update operations succeed without validation errors when valid data is provided.
- **SC-006**: All validation errors for owner, pet, and visit data are clearly communicated to the user.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing `Person` and `NamedEntity` base classes for owner and pet data.
- Data validation will be handled using Jakarta Bean Validation annotations.
- The `id` field for owners, pets, and visits will be auto-generated by the persistence layer.
- The system will use standard Spring MVC patterns for handling web requests and responses.
- The `PetType` entity will be pre-populated or managed separately.
- The `Visit` entity will be associated with a `Pet` which is in turn associated with an `Owner`.
- The `telephone` field will be stored as a string.
- The `birthDate` and `date` fields will be stored in a format compatible with `LocalDate`.
- The system will handle concurrent requests for adding pets with the same name for the same owner by ensuring uniqueness.
- The system will display user-friendly error messages for all validation failures.
- The system will redirect to the appropriate owner list or detail page after successful operations.
- The system will display all owners when a search for an empty last name is performed.
- The system will display a "not found" message when a search yields no results.
- The system will throw `IllegalArgumentException` for non-existent owner IDs when attempting to edit or view.
- The system will throw `IllegalArgumentException` for non-existent pet IDs when attempting to add a visit for a given owner.
- The system will enforce the `\d{10}` pattern for telephone numbers.
- The system will enforce non-blank constraints for first name, last name, address, city, pet name, and visit description.
- The system will enforce the `yyyy-MM-dd` format for birth dates and visit dates.