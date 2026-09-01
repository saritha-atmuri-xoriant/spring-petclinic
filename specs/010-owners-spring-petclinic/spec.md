# Feature Specification: Owner Management for Spring Petclinic

**Feature Branch**: `010-owners-spring-petclinic`

**Created**: 2026-09-01

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find an owner by last name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for accessing owner information and is a primary user journey.

**Independent Test**: Can be fully tested by searching for a known owner's last name and verifying the correct owner details page is displayed.

**Acceptance Scenarios**:

1. **Given** an owner with the last name "Franklin" exists in the system, **When** a user navigates to the owner search page and enters "Franklin" in the last name field, **Then** the system displays the details page for the owner "Franklin".
2. **Given** multiple owners exist, **When** a user searches for owners with the last name "Smith", **Then** the system displays a list of all owners whose last name is "Smith".

---

### User Story 2 - Find all owners when last name search is whitespace (Priority: P2)

Given multiple owners exist, When a user searches for owners with a whitespace-only last name, Then the system displays a list of all owners.

**Why this priority**: This provides a convenient way to view all owners when the specific last name is unknown or when a general overview is needed.

**Independent Test**: Can be fully tested by entering only spaces in the last name search field and verifying all owners are listed.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** a user navigates to the owner search page and enters only whitespace characters in the last name field, **Then** the system displays a list of all registered owners.

---

### User Story 3 - Handle duplicate pet name violation (Priority: P3)

Given an owner exists and has a pet named "Fido", When a user attempts to add a new pet with the name "Fido" for the same owner, Then the system displays an error indicating the pet name already exists.

**Why this priority**: This ensures data integrity and prevents confusion by disallowing duplicate pet names for the same owner.

**Independent Test**: Can be fully tested by creating a pet with a specific name for an owner, then attempting to create another pet with the same name for that same owner and verifying the error message.

**Acceptance Scenarios**:

1. **Given** an owner exists and has a pet named "Fido", **When** a user attempts to add a new pet for that owner and enters "Fido" as the pet's name, **Then** the system displays an error message stating that a pet with this name already exists for this owner.

---

### Edge Cases

- What happens when an owner is created or updated with a blank address? → Validation error is displayed.
- What happens when an owner is created or updated with a blank city? → Validation error is displayed.
- What happens when an owner is created or updated with a telephone number that does not match the 10-digit pattern? → Validation error is displayed.
- What happens when an owner is created or updated with a blank first name? → Validation error is displayed.
- What happens when an owner is created or updated with a blank last name? → Validation error is displayed.
- What happens when attempting to access or update an owner with an ID that does not exist? → An appropriate error indicating the owner was not found is displayed.
- What happens when a pet is created or updated with a blank name? → Validation error is displayed.
- What happens when a pet is created or updated without selecting a pet type? → Validation error is displayed.
- What happens when a pet is created or updated with an invalid birth date? → Validation error is displayed.
- What happens when attempting to save a pet with a name that already exists for the same owner? → Validation error is displayed.
- What happens when creating a visit with a date that is not in the future? → Validation error is displayed.
- What happens when attempting to create a visit for an owner ID that does not exist? → An appropriate error indicating the owner was not found is displayed.
- What happens when attempting to create a visit for a pet ID that does not exist for a given owner? → An appropriate error indicating the pet was not found is displayed.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new owners.
- **FR-002**: System MUST allow updating an existing owner's information (address, city, telephone).
- **FR-003**: System MUST allow the creation of new pets for an owner.
- **FR-004**: System MUST allow updating an existing pet's information (name, birth date, type).
- **FR-005**: System MUST allow viewing a list of pets belonging to an owner.
- **FR-006**: System MUST allow viewing an owner's details, including their associated pets.
- **FR-007**: System MUST validate owner information during creation or update according to defined business rules.
- **FR-008**: System MUST validate pet information during creation or update according to defined business rules.
- **FR-009**: System MUST handle potential data integrity violations when saving owner and pet information.
- **FR-010**: System MUST allow searching for owners by last name.
- **FR-011**: System MUST display all owners when a whitespace-only search is performed for the last name.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (name, address, city, telephone) and a collection of their pets.
- **Pet**: Represents a pet belonging to an owner, including its name, birth date, and type.
- **PetType**: Represents the classification of a pet (e.g., dog, cat).

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully search for and view an owner's details in under 3 seconds.
- **SC-002**: New owners and pets can be created with valid data in under 5 seconds.
- **SC-003**: 95% of users can successfully add or update pet information without encountering validation errors for valid data.
- **SC-004**: The system correctly prevents duplicate pet names for the same owner, providing clear feedback to the user.
- **SC-005**: All mandatory fields for owner and pet creation/update are validated, resulting in a reduction of data entry errors by 90%.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing Person and NamedEntity base classes for Owner and Pet respectively.
- Data validation rules (e.g., phone number format, blank fields) are enforced at the application layer before persistence.
- The system will leverage Spring's built-in validation mechanisms.
- The search functionality for owners by last name will return an empty list if no matching owners are found, rather than an error.