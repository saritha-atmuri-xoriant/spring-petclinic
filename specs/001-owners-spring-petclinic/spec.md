# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `001-owners-spring-petclinic`

**Created**: 2026-09-03

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to be able to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing customer information and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a known owner's last name in the search field and verifying that the correct owner's details are displayed.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists, **When** a user searches for owners with the last name "Franklin", **Then** the system redirects to the owner's details page for "Franklin".
2. **Given** multiple owners share the last name "Smith", **When** a user searches for owners with the last name "Smith", **Then** the system displays a list of all owners with the last name "Smith".
3. **Given** no owner has the last name "NonExistent", **When** a user searches for owners with the last name "NonExistent", **Then** the system displays a message indicating no owners were found.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a new user, I want to be able to create a new owner profile so that I can register my pets with the clinic.

**Why this priority**: This is fundamental for onboarding new clients and expanding the customer base.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying that the owner is created and listed.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with all required fields filled correctly, **Then** the owner is created and the user is redirected to the owner's list page.
2. **Given** a user is on the new owner form, **When** they submit a valid owner form with optional fields filled, **Then** the owner is created with all provided details and the user is redirected to the owner's list page.

---

### User Story 3 - Update an Existing Owner (Priority: P2)

As an existing owner, I want to be able to update my contact information so that the clinic has my most current details.

**Why this priority**: Ensures accurate contact information for communication and record-keeping.

**Independent Test**: Can be fully tested by editing an existing owner's details and verifying that the changes are saved and displayed correctly.

**Acceptance Scenarios**:

1. **Given** an existing owner, **When** the user navigates to the owner's edit page and updates their telephone number, **Then** the new telephone number is saved and displayed on the owner's details page.
2. **Given** an existing owner, **When** the user navigates to the owner's edit page and updates their address, **Then** the new address is saved and displayed on the owner's details page.

---

### User Story 4 - Add a New Pet for an Owner (Priority: P2)

As an owner, I want to add a new pet to my profile so that I can register all my animals with the clinic.

**Why this priority**: Allows owners to manage their pets within the system.

**Independent Test**: Can be fully tested by selecting an owner, navigating to their pet management section, and adding a new pet with valid details.

**Acceptance Scenarios**:

1. **Given** an existing owner, **When** the user navigates to the owner's details page and selects to add a new pet, **Then** a form is presented to enter pet details.
2. **Given** the new pet form is filled with valid pet name and type, **When** the form is submitted, **Then** the new pet is associated with the owner and displayed on the owner's details page.

---

### User Story 5 - View Owner and Pet Details (Priority: P1)

As a clinic staff member or owner, I want to view the details of an owner and their associated pets so that I can have a complete overview of their information.

**Why this priority**: Essential for providing care and managing client relationships.

**Independent Test**: Can be fully tested by searching for an owner and verifying that all their details and their pets' details are displayed correctly.

**Acceptance Scenarios**:

1. **Given** an owner exists with associated pets, **When** the user searches for that owner, **Then** the owner's contact information and a list of their pets (including pet names and types) are displayed.
2. **Given** a pet exists for an owner, **When** viewing the owner's details, **Then** the pet's birth date is displayed.

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
- **Blank Visit Date**: Visit creation/update with a blank date → validation error.
- **Visit Date in the Past**: Visit creation/update with a date that is not after the current date → validation error "typeMismatch.visitDate".
- **Non-existent Owner ID for Visit**: Attempting to add a visit for a pet belonging to a non-existent owner → `IllegalArgumentException` is thrown.
- **Non-existent Pet ID for Visit**: Attempting to add a visit for a non-existent pet belonging to an owner → `IllegalArgumentException` is thrown.
- **Unsaved Owner Data**: Owner creation with errors in fields like address or telephone → form is redisplayed with errors.
- **Unsaved Pet Data**: Pet creation/update with errors in fields like name or type → form is redisplayed with errors.
- **Unsaved Visit Data**: Visit creation/update with errors in fields like date → form is redisplayed with errors.
- **Missing Translation Keys**: If translation files are not in sync, missing keys will be reported.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's contact information (address, city, telephone).
- **FR-003**: System MUST allow finding owners by last name.
- **FR-004**: System MUST allow the creation of a new pet for an existing owner.
- **FR-005**: System MUST allow the update of an existing pet's name and type.
- **FR-006**: System SHOULD validate pet data during creation or update.
- **FR-007**: System SHOULD allow finding owners by last name.
- **FR-008**: System SHOULD allow inserting a new owner.
- **FR-009**: System MUST display a list of pets associated with an owner when viewing owner details.
- **FR-010**: System MUST display owner details including address, city, and telephone.
- **FR-011**: System MUST display pet details including name and type.
- **FR-012**: System MUST validate owner's telephone number format to be exactly 10 digits.
- **FR-013**: System MUST validate pet's name is not blank.
- **FR-014**: System MUST validate pet type is selected.
- **FR-015**: System MUST validate pet's birth date format.
- **FR-016**: System MUST prevent duplicate pet names for the same owner.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner with contact details (first name, last name, address, city, telephone) and a collection of associated pets.
- **Pet**: Represents a pet belonging to an owner, with attributes like name, birth date, and type. It has a relationship with `PetType` and `Owner`.
- **PetType**: Represents the type of a pet (e.g., Cat, Dog). It has a relationship with `Pet`.
- **Visit**: Represents a visit to the clinic for a pet, with attributes like date and description. It has a relationship with `Pet`.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find an owner by last name in under 3 seconds.
- **SC-002**: New owner creation is completed by 95% of users within 2 minutes.
- **SC-003**: 98% of pet creations for existing owners are successful on the first attempt.
- **SC-004**: Owner contact information updates are reflected immediately upon saving.
- **SC-005**: The system successfully handles 100 concurrent requests for owner searches without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The system will use a relational database for persistence.
- Standard web application security practices will be applied.
- The existing `Person` and `NamedEntity` base classes will be utilized for common attributes.
- The `PetClinic Application` will serve as the entry point for this module.
- Translation keys for all user-facing strings will be managed and available.
- The `I18nPropertiesSyncTest` will pass, ensuring translation consistency.
- The `Vet Module` and `System Module` may interact with owner data, but their specific requirements are out of scope for this feature.
- The `Spring Data JPA` will be used for data access.
- `Spring MVC` will be used for handling web requests.
- `Jakarta Validation` will be used for data validation.