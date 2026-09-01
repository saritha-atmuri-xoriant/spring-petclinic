# Feature Specification: Owner Management

**Feature Branch**: `022-owners-spring-petclinic`

**Created**: 2026-09-01

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly find their contact information and associated pets.

**Why this priority**: This is a core functionality for managing customer relationships and is essential for daily operations.

**Independent Test**: Can be fully tested by navigating to the "Find Owners" page, entering a last name, and verifying the displayed list of owners. Delivers the ability to locate specific owners efficiently.

**Acceptance Scenarios**:

1. **Given** there are multiple owners in the system with different last names, **When** I search for an owner using a last name that exists (e.g., "Davis"), **Then** I should see a list of all owners whose last name starts with "Davis".
2. **Given** there are multiple owners in the system, **When** I search for an owner using a last name that does not exist (e.g., "Smithers"), **Then** I should see a message indicating no owners were found.
3. **Given** there are multiple owners with the same last name, **When** I search for that last name, **Then** all owners with that last name should be displayed.

---

### User Story 2 - Create a New Owner (Priority: P2)

As a new user, I want to create a new owner profile so that I can register myself and my pets with the clinic.

**Why this priority**: Essential for onboarding new clients and expanding the clinic's customer base.

**Independent Test**: Can be fully tested by navigating to the "Add Owner" form, filling in all required fields with valid data, and submitting the form. Delivers the ability to add new clients to the system.

**Acceptance Scenarios**:

1. **Given** I am on the "Add Owner" form, **When** I enter valid details for first name, last name, address, city, and telephone, **Then** the owner profile should be created successfully, and I should be redirected to the owner's details page or the owner list.
2. **Given** I am on the "Add Owner" form, **When** I leave a mandatory field blank (e.g., first name), **Then** I should see a validation error message for that field, and the owner should not be created.
3. **Given** I am on the "Add Owner" form, **When** I enter an invalid telephone number format (e.g., "123"), **Then** I should see a validation error message for the telephone field, and the owner should not be created.

---

### User Story 3 - Edit an Existing Owner (Priority: P3)

As an existing owner, I want to edit my profile information so that I can keep my contact details up-to-date.

**Why this priority**: Important for maintaining accurate client records and ensuring effective communication.

**Independent Test**: Can be fully tested by finding an existing owner, navigating to their edit page, modifying a field (e.g., address), and submitting the changes. Delivers the ability to update existing client information.

**Acceptance Scenarios**:

1. **Given** I have an existing owner profile, **When** I navigate to the "Edit Owner" page and update my address and city with valid information, **Then** the owner's details should be updated successfully, and I should see the updated information displayed.
2. **Given** I am on the "Edit Owner" page, **When** I attempt to clear a mandatory field (e.g., last name), **Then** I should see a validation error message, and the changes should not be saved.

---

### User Story 4 - Add a New Pet to an Existing Owner (Priority: P1)

As an existing owner, I want to add a new pet to my profile so that I can register my pet with the clinic.

**Why this priority**: Core functionality for pet owners to manage their pets within the system.

**Independent Test**: Can be fully tested by finding an existing owner, navigating to their pet management section, and adding a new pet with valid details. Delivers the ability to associate new pets with existing owners.

**Acceptance Scenarios**:

1. **Given** I am viewing an existing owner's profile, **When** I choose to add a new pet and provide a valid name, birth date, and select a pet type, **Then** the new pet should be successfully added to the owner's profile.
2. **Given** I am adding a new pet, **When** I enter a pet name that already exists for this owner, **Then** I should see a validation error indicating the pet name must be unique for this owner.
3. **Given** I am adding a new pet, **When** I do not select a pet type, **Then** I should see a validation error indicating that a pet type must be selected.

---

### User Story 5 - Edit an Existing Pet's Information (Priority: P2)

As an owner, I want to edit my pet's information so that I can correct any inaccuracies or update details like the birth date or type.

**Why this priority**: Ensures the accuracy of pet records, which is crucial for veterinary care.

**Independent Test**: Can be fully tested by finding an owner, selecting one of their pets, navigating to the pet edit page, changing a detail (e.g., birth date), and saving. Delivers the ability to correct pet information.

**Acceptance Scenarios**:

1. **Given** an owner has an existing pet, **When** I navigate to the pet's edit page and update its birth date, **Then** the pet's birth date should be updated successfully.
2. **Given** an owner has an existing pet, **When** I navigate to the pet's edit page and change its pet type, **Then** the pet's type should be updated successfully.
3. **Given** I am editing a pet's information, **When** I attempt to enter an invalid birth date format, **Then** I should see a validation error.

---

### Edge Cases

- What happens when an owner is created or updated with a blank first name? → Validation error.
- What happens when an owner is created or updated with a blank last name? → Validation error.
- What happens when an owner is created or updated with an invalid telephone format? → Validation error.
- What happens when an owner is created or updated with a blank address? → Validation error.
- What happens when an owner is created or updated with a blank city? → Validation error.
- What happens when attempting to edit or view an owner with a non-existent ID? → `IllegalArgumentException` is thrown.
- What happens when a pet is created or updated with a blank name? → Validation error.
- What happens when a pet is created or updated without selecting a pet type? → Validation error.
- What happens when a pet is created or updated with a null birth date? → Validation error.
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error.
- What happens when attempting to create a visit for an owner ID that does not exist? → `IllegalArgumentException` is thrown.
- What happens when attempting to create a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` is thrown.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow updating an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD display a list of pet types when creating or updating a pet.
- **FR-005**: System SHOULD handle potential data integrity violations when saving owner or pet data.
- **FR-006**: System MUST allow searching for owners by last name.
- **FR-007**: System MUST allow creating new owner profiles.
- **FR-008**: System MUST allow editing existing owner profiles.
- **FR-009**: System MUST enforce validation rules for owner fields (first name, last name, address, city, telephone).
- **FR-010**: System MUST enforce validation rules for pet fields (name, birth date, pet type).

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal contact information and a collection of their pets. Attributes include first name, last name, address, city, and telephone number.
- **Pet**: Represents an animal owned by a person, including its name, birth date, and type. It is associated with an Owner and can have multiple Visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat, bird).
- **Visit**: Represents a veterinary visit for a pet, including the date and a description of the service provided.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name in under 3 seconds.
- **SC-002**: New owner creation process takes less than 1 minute for a user with valid information.
- **SC-003**: 95% of owner and pet data updates are successfully processed without errors.
- **SC-004**: The system correctly validates all owner and pet fields, with validation errors displayed clearly to the user.
- **SC-005**: The number of support tickets related to incorrect or missing owner/pet information decreases by 30% within one quarter of release.

## Assumptions

- Users have stable internet connectivity when accessing the application.
- The application will be accessed via a web browser.
- The system will reuse existing authentication mechanisms if applicable (though not explicitly detailed in the provided context).
- Data integrity for relationships between owners, pets, and visits will be maintained by the persistence layer.
- The list of available `PetType`s is managed separately and will be available for selection.