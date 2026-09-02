# Feature Specification: Owner Management

**Feature Branch**: `005-owners-spring-petclinic`

**Created**: 2026-09-02

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given owners exist in the system, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for navigating and managing pet owners, enabling quick access to specific owner records.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the displayed list of owners.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for owners with the last name prefix "Sm", **Then** the system displays owners "Smith" and "Smythe".
2. **Given** there are no owners with the last name "Davis", **When** the user searches for owners with the last name prefix "Dav", **Then** the system displays a message indicating no owners were found.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's detail page.

**Why this priority**: This is essential for onboarding new pet owners into the system.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying redirection to the newly created owner's detail page.

**Acceptance Scenarios**:

1. **Given** the user is on the "New Owner" form, **When** they enter valid details for address, city, telephone, first name, and last name, and submit the form, **Then** the owner is successfully created and the user is redirected to the detail page for that new owner.

---

### User Story 3 - View Owner List (Priority: P2)

Given owners exist in the system, When a user navigates to the owners list page, Then all owners are displayed in a paginated list.

**Why this priority**: Provides an overview of all registered owners, facilitating general management and discovery.

**Independent Test**: Can be fully tested by navigating to the owners list page and verifying that all existing owners are displayed, with pagination if the list is long.

**Acceptance Scenarios**:

1. **Given** there are 20 owners in the system, **When** the user navigates to the "Owners" list page, **Then** the system displays the first 10 owners, with pagination controls to view the next set.

---

### User Story 4 - Update Existing Owner (Priority: P2)

Given a user is viewing an existing owner's detail page, When they edit and submit valid owner information, Then the owner's details are updated.

**Why this priority**: Allows for maintaining accurate and up-to-date owner information.

**Independent Test**: Can be fully tested by editing an owner's details on their detail page and verifying the changes are saved.

**Acceptance Scenarios**:

1. **Given** the user is on the detail page for "John Smith", **When** they change his telephone number and submit the form, **Then** the owner's detail page now shows the updated telephone number.

---

### User Story 5 - Add a New Pet to an Owner (Priority: P3)

Given a user is viewing an owner's detail page, When they add a new pet for that owner, Then the pet is associated with the owner.

**Why this priority**: Enables owners to register new pets within the system.

**Independent Test**: Can be fully tested by navigating to an owner's detail page, initiating the "Add Pet" action, filling in pet details, and verifying the new pet appears on the owner's profile.

**Acceptance Scenarios**:

1. **Given** the user is on the detail page for "Jane Doe", **When** they add a new pet named "Buddy" with a birth date and type "Dog", **Then** "Buddy" appears in the list of pets for "Jane Doe".

---

### User Story 6 - Add a New Visit for a Pet (Priority: P3)

Given a user is viewing a pet's detail page, When they add a new visit for that pet, Then the visit is recorded and associated with the pet.

**Why this priority**: Tracks the medical history and interactions of pets with the clinic.

**Independent Test**: Can be fully tested by navigating to a pet's detail page, initiating the "Add Visit" action, filling in visit details, and verifying the new visit is recorded.

**Acceptance Scenarios**:

1. **Given** the user is on the detail page for "Buddy" (owned by Jane Doe), **When** they add a visit with today's date and a description "Annual check-up", **Then** the visit is recorded and displayed on Buddy's visit history.

---

### Edge Cases

- What happens when an owner is created/updated with a blank address?
  - **Expected Outcome**: Validation error is displayed, and the owner is not saved.
- What happens when an owner is created/updated with a blank city?
  - **Expected Outcome**: Validation error is displayed, and the owner is not saved.
- What happens when an owner is created/updated with a telephone number that is not exactly 10 digits?
  - **Expected Outcome**: Validation error is displayed, and the owner is not saved.
- What happens when attempting to access or modify an owner with an ID that does not exist?
  - **Expected Outcome**: An `IllegalArgumentException` is thrown, and an appropriate error message is displayed to the user.
- What happens when a pet is created/updated with a blank name?
  - **Expected Outcome**: Validation error is displayed, and the pet is not saved.
- What happens when a pet is created/updated without selecting a pet type?
  - **Expected Outcome**: Validation error is displayed, and the pet is not saved.
- What happens when a pet is created/updated with a null birth date?
  - **Expected Outcome**: Validation error is displayed, and the pet is not saved.
- What happens when attempting to add a pet with a name that already exists for the same owner?
  - **Expected Outcome**: Validation error is displayed, and the pet is not saved.
- What happens when a visit is created/updated with a date that is not after the current date?
  - **Expected Outcome**: Validation error is displayed, and the visit is not saved.
- What happens when attempting to create a visit for a pet ID that does not exist for a given owner?
  - **Expected Outcome**: An `IllegalArgumentException` is thrown, and an appropriate error message is displayed to the user.
- What happens when searching for owners by last name when no owners match the criteria?
  - **Expected Outcome**: A message indicating "no owners found" is displayed.
- What happens when navigating to the "/oups" endpoint?
  - **Expected Outcome**: A `RuntimeException` is thrown, showcasing exception handling.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST allow the update of an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD allow searching for owners by last name.
- **FR-005**: System SHOULD allow adding new visits for a pet.
- **FR-006**: System MUST allow the creation of a new owner.
- **FR-007**: System MUST allow the update of an existing owner's details (address, city, telephone).
- **FR-008**: System MUST display a list of all owners, with pagination.
- **FR-009**: System MUST display owner details, including their associated pets and visits.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including their personal details (address, city, telephone) and a list of their pets.
- **Pet**: Represents an animal owned by a pet owner, including its birth date, type, and a history of visits.
- **PetType**: Represents the category of a pet (e.g., dog, cat).
- **Visit**: Represents a record of a pet's interaction with the clinic, including the date and a description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 2 seconds.
- **SC-002**: New owners can be created with valid data in under 30 seconds.
- **SC-003**: The owner list page loads with all owners (or paginated set) in under 3 seconds.
- **SC-004**: Adding a new pet to an owner is completed within 15 seconds.
- **SC-005**: Adding a new visit for a pet is completed within 15 seconds.
- **SC-006**: 95% of owner data updates are successfully persisted and reflected immediately.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing Person and NamedEntity base classes for Owner and Pet respectively.
- Data validation for owner and pet details will follow the constraints defined in the repository context (e.g., 10-digit phone number, non-blank fields).
- The system will use standard web application patterns for displaying lists and details.
- The system will leverage Spring Data JPA for persistence.
- The system will use standard date formatting for pet birth dates and visit dates.
- The system will handle exceptions gracefully, providing user-friendly error messages.
- The system will support at least 10 concurrent users performing owner management operations without performance degradation.