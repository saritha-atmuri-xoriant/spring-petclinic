# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `002-owners-spring-petclinic`

**Created**: 2026-09-04

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly access their information.

**Why this priority**: This is a core functionality for managing owners and is essential for daily operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list of owners.

**Acceptance Scenarios**:

1. **Given** a list of owners exists with various last names, **When** I search for owners using the prefix "Sm", **Then** a list of owners whose last names start with "Sm" (e.g., Smith, Smothers) is displayed.
2. **Given** a list of owners exists, **When** I search for an owner last name that does not exist (e.g., "XYZ"), **Then** a message indicating "No owners found" is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a clinic staff member, I want to create a new owner record so that I can register new clients and their pets.

**Why this priority**: Essential for onboarding new clients into the system.

**Independent Test**: Can be fully tested by filling out the owner creation form with valid data and verifying the owner is created and displayed on their details page.

**Acceptance Scenarios**:

1. **Given** I am on the owner creation form, **When** I enter valid first name, last name, address, city, and telephone number, and click "Save", **Then** the new owner is created and I am redirected to the owner's details page.
2. **Given** I am on the owner creation form, **When** I leave the first name blank and click "Save", **Then** a validation error message "First name must not be blank" is displayed, and the form remains open.

---

### User Story 3 - Add a New Pet to an Owner (Priority: P2)

As a clinic staff member, I want to add a new pet to an existing owner's record so that I can track their pets' information and visits.

**Why this priority**: Important for managing a pet owner's complete profile.

**Independent Test**: Can be fully tested by navigating to an owner's details page, initiating the pet addition, filling out the pet form with valid data, and verifying the pet is added to the owner's list.

**Acceptance Scenarios**:

1. **Given** I am viewing an owner's details page, **When** I click "Add New Pet", fill in the pet's name, select a pet type, and enter a birth date, and click "Save", **Then** the new pet is added to the owner's profile.
2. **Given** I am viewing an owner's details page, **When** I attempt to add a pet with a name that already exists for this owner (e.g., "Buddy" already exists, and I try to add another "Buddy"), **Then** a validation error message "Pet name must be unique for this owner" is displayed, and the form remains open.

---

### User Story 4 - Add a Visit for a Pet (Priority: P2)

As a clinic staff member, I want to add a visit record for a pet so that I can track their medical history.

**Why this priority**: Crucial for maintaining a pet's medical history.

**Independent Test**: Can be fully tested by navigating to a pet's details, initiating a visit addition, filling in the visit date and description, and verifying the visit is recorded.

**Acceptance Scenarios**:

1. **Given** I am viewing a pet's details, **When** I click "Add New Visit", enter a valid date and description, and click "Save", **Then** the new visit is recorded and displayed in the pet's visit history.
2. **Given** I am viewing a pet's details, **When** I attempt to add a visit with a blank description, **Then** a validation error message "Visit description must not be blank" is displayed, and the form remains open.

---

### User Story 5 - Update an Existing Owner (Priority: P3)

As a clinic staff member, I want to update an existing owner's information so that I can keep their contact details current.

**Why this priority**: Ensures data accuracy for existing clients.

**Independent Test**: Can be fully tested by finding an owner, navigating to their edit page, modifying a field (e.g., telephone), saving, and verifying the change.

**Acceptance Scenarios**:

1. **Given** I am viewing an owner's details, **When** I click "Edit Owner", change the telephone number to a valid 10-digit number, and click "Save", **Then** the owner's telephone number is updated.
2. **Given** I am viewing an owner's details, **When** I click "Edit Owner", clear the address field, and click "Save", **Then** a validation error message "Address must not be blank" is displayed, and the form remains open.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **Owner Not Found During Find**: Searching for an owner by last name that yields no results → validation error "notFound" for lastName.
- **Blank Pet Name**: Pet creation/update with a blank name → validation error "required".
- **Missing Pet Type**: Pet creation/update without selecting a pet type → validation error "required".
- **Invalid Pet Birth Date Format**: Pet creation/update with a birth date not in the expected format (e.g., "2015/02/12") → validation error "typeMismatch".
- **Duplicate Pet Name for Same Owner**: Attempting to add a pet with a name that already exists for the same owner → validation error "duplicate".
- **Invalid Visit Date**: Visit submission with a date that is not in the future → validation error "typeMismatch.visitDate".
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet ID that does not exist for the specified owner → `IllegalArgumentException` is thrown.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow updating existing owner information (first name, last name, address, city, telephone).
- **FR-003**: System MUST allow searching for owners by last name prefix.
- **FR-004**: System MUST allow the creation of new pets for an owner.
- **FR-005**: System MUST allow updating an existing pet's name.
- **FR-006**: System MUST allow adding a new visit for a pet.
- **FR-007**: System MUST validate owner data during creation or update according to defined business rules.
- **FR-008**: System MUST validate pet data during creation or update according to defined business rules.
- **FR-009**: System MUST validate visit data during creation according to defined business rules.
- **FR-010**: System MUST prevent duplicate pet names for the same owner.
- **FR-011**: System SHOULD provide a welcome page at the root URL.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including contact details and a list of their pets. Attributes include first name, last name, address, city, and telephone.
- **Pet**: Represents a pet belonging to an owner. Attributes include name, birth date, and type. It has a relationship with Owner and Visit.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a veterinary visit for a pet, including date and description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 3 seconds.
- **SC-002**: New owner creation and redirection to the owner's details page completes in under 5 seconds.
- **SC-003**: Adding a new pet to an owner's record is completed and reflected on the owner's details page in under 5 seconds.
- **SC-004**: 95% of owner data validation errors are displayed to the user immediately upon form submission.
- **SC-005**: The system successfully handles 100 concurrent requests for owner searches without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- Standard web application security practices will be followed for data handling.
- The existing database schema for owners, pets, and visits will be utilized.
- The application language is English by default.
- The telephone number format `\d{10}` is sufficient for all supported regions.
- The date format for pet birth dates and visit dates is `yyyy-MM-dd`.
- The system will be deployed in an environment where the database is accessible.