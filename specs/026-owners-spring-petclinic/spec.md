# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `026-owners-spring-petclinic`

**Created**: 2026-08-29

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given an owner with the last name "Franklin" exists, When a user searches for owners with the last name "Franklin", Then the system redirects to the owner's details page.

**Why this priority**: This is a core functionality for managing and accessing owner information, essential for day-to-day operations.

**Independent Test**: Can be fully tested by searching for a known owner's last name and verifying the correct owner details page is displayed. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** an owner named "John Franklin" exists, **When** the user searches for owners with the last name "Franklin", **Then** the system displays the details for John Franklin.
2. **Given** multiple owners exist with the last name "Smith", **When** the user searches for owners with the last name "Smith", **Then** the system displays a list of all owners with the last name "Smith".

---

### User Story 2 - Find Owners with Partial Last Name Match (Priority: P2)

Given multiple owners exist whose last names start with "Frank", When a user searches for owners with the last name "Frank", Then a list of owners matching the partial name is displayed.

**Why this priority**: This enhances usability by allowing users to find owners even if they don't know the exact spelling or full last name.

**Independent Test**: Can be fully tested by searching for a partial last name that matches multiple existing owners and verifying that all relevant owners are listed. Delivers the ability to find owners with incomplete name information.

**Acceptance Scenarios**:

1. **Given** owners "Frank Smith", "Frank Jones", and "John Doe" exist, **When** the user searches for owners with the last name "Frank", **Then** the system displays a list containing "Frank Smith" and "Frank Jones".

---

### User Story 3 - Handle Empty Last Name Search (Priority: P3)

Given multiple owners exist, When a user searches for owners with an empty or whitespace-only last name, Then all owners are displayed in a list.

**Why this priority**: This ensures that users can retrieve a complete list of all owners if no specific search criteria are provided, serving as a fallback for browsing.

**Independent Test**: Can be fully tested by performing a search with an empty last name field and verifying that all existing owners are displayed. Delivers the ability to view all registered owners.

**Acceptance Scenarios**:

1. **Given** multiple owners exist in the system, **When** the user performs a search with an empty last name field, **Then** the system displays a list of all owners.

---

### Edge Cases

- What happens when an owner's first name is blank? → Validation error.
- What happens when an owner's telephone number is not 10 digits? → Validation error.
- How does the system handle attempts to edit an owner that does not exist? → `IllegalArgumentException` indicating owner not found.
- How does the system handle attempts to add a pet with a name that already exists for the same owner? → Validation error "duplicate".
- How does the system handle booking a visit with a date that is not after the current date? → Validation error "typeMismatch.visitDate".

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new owner.
- **FR-002**: System MUST allow the update of an existing owner's details (address, city, telephone).
- **FR-003**: System MUST allow the creation of a new pet for a given owner.
- **FR-004**: System MUST allow the update of an existing pet's name and birth date.
- **FR-005**: System MUST allow the creation of a new visit for a given pet.
- **FR-006**: System MUST allow the update of an existing visit's date.
- **FR-007**: System MUST validate owner information during creation or update, enforcing non-blank fields for first name, last name, address, and city, and a 10-digit format for telephone.
- **FR-008**: System MUST validate pet information during creation or update, enforcing non-blank names and valid birth dates.
- **FR-009**: System MUST validate visit information during creation or update, enforcing non-blank descriptions and valid dates.
- **FR-010**: System MUST prevent duplicate pet names for the same owner.
- **FR-011**: System MUST retrieve a list of available pet types for selection when adding or editing a pet.
- **FR-012**: System MUST handle potential data integrity violations when saving owner, pet, or visit information.
- **FR-013**: System MUST allow searching for owners by last name, including partial matches and displaying all owners when the search term is empty.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner, including personal details (address, city, telephone) and a collection of associated pets.
- **Pet**: Represents a pet, including its name, birth date, type, and a history of visits.
- **PetType**: Represents the classification of a pet (e.g., dog, cat).
- **Visit**: Represents a record of a pet's visit to the clinic, including the date.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can successfully create, update, and view owner details in under 1 minute per operation.
- **SC-002**: Users can successfully add, update, and view pet details for an owner in under 2 minutes per operation.
- **SC-003**: Users can successfully add and view visits for a pet in under 1.5 minutes per operation.
- **SC-004**: Owner search functionality returns results within 3 seconds for any valid last name query.
- **SC-005**: 95% of owner, pet, and visit creation/update operations complete without validation errors due to incorrect data formats or missing required fields.

## Assumptions

- Users have stable internet connectivity.
- The system will reuse existing `Person` entity for owner's first and last name.
- The system will reuse existing `NamedEntity` for pet names and pet types.
- The system will reuse existing `BaseEntity` for visit IDs.
- The system will use standard date formats for `LocalDate`.
- The system will use industry-standard validation messages for errors.
- Mobile support is out of scope for this iteration.
- The `spring-petclinic` application will be the primary consumer of these owner management features.
- The `I18nPropertiesSyncTest` will pass, ensuring all user-facing strings are correctly internationalized.
- The project will be built using Maven and Java 17 or later.
- Data persistence will be handled by Spring Data JPA repositories.