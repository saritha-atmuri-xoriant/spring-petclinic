# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `004-owners-spring-petclinic`

**Created**: 2026-08-31

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

As a clinic staff member, I want to search for owners by their last name so that I can quickly find their contact information and pet details.

**Why this priority**: This is a core functionality for managing customer relationships and is likely the most frequent operation for staff.

**Independent Test**: Can be fully tested by navigating to the owner search page, entering a last name prefix, and verifying the returned list. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** there are owners in the system with last names "Smith", "Smythe", and "Jones", **When** a user searches for owners with the last name prefix "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** there are no owners with the last name "Davis", **When** a user searches for owners with the last name prefix "Dav", **Then** a message indicating "Owner not found" is displayed.

---

### User Story 2 - Create a New Owner (Priority: P1)

As a new user, I want to create a new owner profile so that I can register myself or a new client with the clinic.

**Why this priority**: Essential for onboarding new clients and expanding the clinic's customer base.

**Independent Test**: Can be fully tested by navigating to the new owner form, filling in valid details, and submitting. Delivers the ability to add new clients.

**Acceptance Scenarios**:

1. **Given** a user is on the new owner form, **When** they submit a valid owner form with first name "John", last name "Doe", address "123 Main St", city "Anytown", and telephone "1234567890", **Then** the owner "John Doe" is created and the user is redirected to their details page.
2. **Given** a user is on the new owner form, **When** they submit the form with a blank address, **Then** a validation error is displayed for the address field, and the owner is not created.

---

### User Story 3 - View a List of All Owners (Priority: P2)

As a clinic staff member, I want to view a list of all registered owners so that I can get an overview of the client base.

**Why this priority**: Provides a general overview and is useful for administrative tasks and reporting.

**Independent Test**: Can be fully tested by navigating to the owners list page and verifying that a list of owners is displayed. Delivers visibility into the client roster.

**Acceptance Scenarios**:

1. **Given** there are multiple owners registered in the system, **When** a user navigates to the owners list page, **Then** all owners are displayed in a paginated list, showing at least their first name, last name, and city.

---

### User Story 4 - Add a New Pet for an Existing Owner (Priority: P2)

As a clinic staff member, I want to add a new pet to an existing owner's profile so that I can keep track of all their animals.

**Why this priority**: Crucial for maintaining accurate pet records, which is central to veterinary care.

**Independent Test**: Can be fully tested by selecting an existing owner, navigating to their pet management section, and adding a new pet with valid details. Delivers the ability to associate pets with owners.

**Acceptance Scenarios**:

1. **Given** an owner "Jane Smith" exists, **When** a user adds a new pet named "Buddy", a "Dog", born on "2020-05-15" to Jane Smith's profile, **Then** "Buddy" appears in Jane Smith's list of pets.
2. **Given** an owner "Jane Smith" exists, **When** a user attempts to add a pet with a blank name, **Then** a validation error is displayed for the pet's name, and the pet is not added.

---

### User Story 5 - Update an Existing Pet's Information (Priority: P3)

As a clinic staff member, I want to update an existing pet's information so that I can correct any inaccuracies or record changes.

**Why this priority**: Ensures the accuracy of pet records, which is important for treatment and history.

**Independent Test**: Can be fully tested by selecting an existing pet, editing its details (e.g., birth date), and saving the changes. Delivers the ability to maintain accurate pet data.

**Acceptance Scenarios**:

1. **Given** a pet "Buddy" owned by "Jane Smith" exists with a birth date of "2020-05-15", **When** the user updates Buddy's birth date to "2020-06-20", **Then** the pet's birth date is updated to "2020-06-20".
2. **Given** a pet "Buddy" owned by "Jane Smith" exists, **When** the user attempts to update Buddy's name to a name that already exists for another pet owned by Jane Smith, **Then** a validation error is displayed for the duplicate pet name, and the update fails.

---

### Edge Cases

- What happens when an owner is created or updated with a blank address? → Validation error.
- What happens when an owner is created or updated with a blank city? → Validation error.
- What happens when an owner's telephone number does not match the 10-digit pattern? → Validation error.
- What happens when a user attempts to access or modify an owner with a non-existent ID? → `IllegalArgumentException` is thrown.
- What happens when a pet is created or updated with a blank name? → Validation error.
- What happens when a pet is created or updated without selecting a pet type? → Validation error.
- What happens when a pet is created or updated with a null birth date? → Validation error.
- What happens when attempting to add a pet with a name that already exists for the same owner? → Validation error.
- What happens when a visit is created with a date that is not in the future? → Validation error.
- What happens when attempting to create a visit for a pet ID that does not exist for a given owner? → `IllegalArgumentException` is thrown.
- What happens when searching for owners by last name yields no results? → Validation error "notFound" on the lastName field.
- What happens when accessing the "/oups" endpoint? → `RuntimeException` is thrown, leading to an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow users to create a new pet for an existing owner.
- **FR-002**: System MUST allow users to update an existing pet's information.
- **FR-003**: System SHOULD validate pet data before saving.
- **FR-004**: System SHOULD populate a list of available pet types when creating or updating a pet.
- **FR-005**: System SHOULD handle cases where an owner is not found when attempting to add or update a pet.
- **FR-006**: System MUST allow users to find owners by last name prefix.
- **FR-007**: System MUST allow users to create a new owner profile.
- **FR-008**: System MUST allow users to view a paginated list of all owners.
- **FR-009**: System MUST validate owner details (first name, last name, address, city, telephone) upon creation or update.
- **FR-010**: System MUST validate pet details (name, type, birth date) upon creation or update.
- **FR-011**: System MUST ensure pet names are unique within an owner's profile.
- **FR-012**: System MUST allow users to add visits for existing pets.
- **FR-013**: System MUST validate visit details (date, description).
- **FR-014**: System MUST display user-friendly error messages for validation failures.
- **FR-015**: System MUST handle exceptions gracefully, such as when accessing the "/oups" endpoint.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a clinic client, including their contact information (first name, last name, address, city, telephone) and associated pets.
- **Pet**: Represents an animal belonging to an owner, including its name, birth date, and type.
- **PetType**: Represents the category of a pet (e.g., Dog, Cat, Hamster).
- **Visit**: Represents a veterinary visit for a pet, including the date and a description of the visit.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 3 seconds.
- **SC-002**: New owner creation and redirection to the owner's details page completes in under 5 seconds.
- **SC-003**: The list of all owners loads and displays paginated results within 4 seconds.
- **SC-004**: Adding a new pet to an owner's profile is completed and reflected in the UI within 4 seconds.
- **SC-005**: Updating an existing pet's information is completed and reflected in the UI within 4 seconds.
- **SC-006**: 95% of form submissions (owner, pet, visit) with invalid data result in clear, actionable validation messages presented to the user.
- **SC-007**: The system can handle up to 500 concurrent users browsing the owner list without performance degradation.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- The primary users are clinic staff members and potentially new clients registering.
- Data persistence is handled by an underlying database (e.g., MySQL, PostgreSQL) as implied by Spring Data JPA usage.
- Standard web application security practices will be applied to protect user data.
- The internationalization (i18n) requirements will be met for all user-facing strings.