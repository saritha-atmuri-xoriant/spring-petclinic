# Feature Specification: Owners for Spring Petclinic

**Feature Branch**: `[001-owners-for-spring-petclinic]`

**Created**: 2026-09-01

**Status**: Draft

**Input**: User description: "owners for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Find Owners by Last Name (Priority: P1)

Given owners exist in the system, When a user searches for owners by a last name prefix, Then a list of owners whose last names start with that prefix is displayed.

**Why this priority**: This is a core functionality for navigating and managing owner data, essential for basic operations.

**Independent Test**: Can be fully tested by entering a last name prefix in the search field and verifying the returned list. Delivers the ability to locate specific owners.

**Acceptance Scenarios**:

1. **Given** there are owners with last names "Smith", "Smythe", and "Jones", **When** the user searches for owners with the last name prefix "Sm", **Then** a list containing "Smith" and "Smythe" is displayed.
2. **Given** there are no owners with the last name "Davis", **When** the user searches for owners with the last name prefix "Dav", **Then** a "not found" message is displayed for the last name field.

---

### User Story 2 - Create a New Owner (Priority: P1)

Given a user is on the new owner form, When they submit a valid owner form, Then the owner is created and redirected to the owner's details page.

**Why this priority**: This is fundamental for adding new clients to the clinic.

**Independent Test**: Can be fully tested by filling out the new owner form with valid data and verifying redirection to the owner's detail page. Delivers the ability to onboard new clients.

**Acceptance Scenarios**:

1. **Given** the user is on the "Add Owner" page, **When** they fill in all required fields (first name, last name, address, city, telephone) with valid data and click "Save", **Then** the owner is created and the user is redirected to the newly created owner's details page.

---

### User Story 3 - View Owner List (Priority: P2)

Given owners exist in the system, When a user navigates to the owners list page, Then all owners are displayed in a paginated list.

**Why this priority**: Provides an overview of all registered owners, useful for administrative tasks and general reference.

**Independent Test**: Can be fully tested by navigating to the owners list page and verifying that owners are displayed, potentially across multiple pages if there are many. Delivers a comprehensive view of the client base.

**Acceptance Scenarios**:

1. **Given** there are more than 10 owners in the system, **When** the user navigates to the owners list page, **Then** the first 10 owners are displayed, along with pagination controls to view subsequent pages.

---

### User Story 4 - View Owner Details (Priority: P2)

Given an owner exists in the system, When a user navigates to the owner's details page, Then the owner's information and their associated pets are displayed.

**Why this priority**: Allows users to see all relevant information about a specific owner and their pets in one place.

**Independent Test**: Can be fully tested by selecting an owner from the list or search results and verifying their details and pets are shown. Delivers a consolidated view of an owner's record.

**Acceptance Scenarios**:

1. **Given** an owner named "John Doe" exists with pets "Buddy" (Dog) and "Whiskers" (Cat), **When** the user navigates to John Doe's details page, **Then** the owner's name, address, city, telephone, and a list of their pets (Buddy, Whiskers) are displayed.

---

### User Story 5 - Create a New Pet for an Owner (Priority: P2)

Given an owner exists, When a user navigates to the owner's details page and initiates pet creation, Then they can add a new pet with its details.

**Why this priority**: Essential for pet owners to register new pets with the clinic.

**Independent Test**: Can be fully tested by selecting an owner, initiating pet creation, filling in pet details, and verifying the pet is added to the owner's record. Delivers the ability to manage an owner's pets.

**Acceptance Scenarios**:

1. **Given** an owner "Jane Smith" exists, **When** the user navigates to Jane Smith's details page, clicks "Add New Pet", fills in the pet's name, birth date, and selects a pet type (e.g., "Dog"), and clicks "Save", **Then** the new pet is associated with Jane Smith and appears on her details page.

---

### User Story 6 - Update an Existing Pet's Information (Priority: P3)

Given a pet exists for an owner, When a user navigates to the pet's details and initiates an update, Then they can modify the pet's information.

**Why this priority**: Allows for correction of errors or updating details of existing pets.

**Independent Test**: Can be fully tested by selecting a pet, editing its details (e.g., name, birth date), and verifying the changes are saved. Delivers the ability to maintain accurate pet records.

**Acceptance Scenarios**:

1. **Given** a pet named "Buddy" (Dog) exists for owner "John Doe", **When** the user navigates to Buddy's details, changes the name to "Buddy Jr." and updates the birth date, and clicks "Save", **Then** the pet's record is updated to reflect the new name and birth date.

---

### User Story 7 - Add a Visit for a Pet (Priority: P3)

Given a pet exists for an owner, When a user navigates to the pet's details and initiates visit booking, Then they can add a new visit with its date and description.

**Why this priority**: Crucial for tracking veterinary appointments and services.

**Independent Test**: Can be fully tested by selecting a pet, booking a visit with a valid date and description, and verifying it appears in the visit history. Delivers the ability to record pet visits.

**Acceptance Scenarios**:

1. **Given** a pet "Buddy" exists for owner "John Doe", **When** the user navigates to Buddy's details, clicks "Add New Visit", enters a visit date and a description "Annual check-up", and clicks "Save", **Then** the visit is recorded and associated with Buddy.

---

### Edge Cases

- **Blank First Name**: Owner creation/update with a blank first name → validation error.
- **Blank Last Name**: Owner creation/update with a blank last name → validation error.
- **Invalid Telephone Format**: Owner creation/update with a telephone number not matching the `\d{10}` pattern → validation error.
- **Blank Address**: Owner creation/update with a blank address → validation error.
- **Blank City**: Owner creation/update with a blank city → validation error.
- **Non-existent Owner ID**: Attempting to edit or view an owner with an ID that does not exist → `IllegalArgumentException` is thrown.
- **No Owners Found**: Searching for owners with a last name that yields no results → error message "not found" is added to the `lastName` field, and the `findOwners` view is returned.
- **Blank Pet Name**: Creating or updating a pet with a blank name → validation error "required".
- **Missing Pet Type**: Creating a pet without specifying a type → validation error "required".
- **Invalid Pet Birth Date Format**: Creating or updating a pet with a birth date in an incorrect format (e.g., "2015/02/12") → validation error "typeMismatch".
- **Duplicate Pet Name for Same Owner**: Attempting to save a pet with a name that already exists for the same owner → validation error "duplicate".
- **Invalid Visit Date**: Booking a visit with a date that is not in the future → validation error "typeMismatch.visitDate".
- **Non-existent Pet ID for Owner**: Attempting to add a visit for a pet ID that does not exist for a given owner → `IllegalArgumentException` is thrown.
- **Exception Trigger**: Accessing the `/oups` endpoint → a `RuntimeException` is thrown, resulting in an internal server error.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of new pets for an existing owner.
- **FR-002**: System MUST allow updating an existing pet's name.
- **FR-003**: System SHOULD validate pet information during creation or update.
- **FR-004**: System SHOULD display a form for creating or updating pet details.
- **FR-005**: System SHOULD populate a list of available pet types for selection during pet creation/update.
- **FR-006**: System MUST allow searching for owners by last name prefix.
- **FR-007**: System MUST allow creation of new owners.
- **FR-008**: System MUST display a list of all owners, with pagination.
- **FR-009**: System MUST display detailed information for a selected owner, including their pets.
- **FR-010**: System MUST allow booking a visit for a pet, including date and description.
- **FR-011**: System MUST validate owner details upon creation/update, including address, city, and telephone format.
- **FR-012**: System MUST validate pet details upon creation/update, including name and birth date format.
- **FR-013**: System MUST prevent duplicate pet names for the same owner.
- **FR-014**: System MUST validate visit dates to ensure they are in the future.

### Key Entities *(include if feature involves data)*

- **Owner**: Represents a pet owner. Attributes include first name, last name, address, city, and telephone number. Has a one-to-many relationship with `Pet`.
- **Pet**: Represents a pet. Attributes include name, birth date, and type. Has a many-to-one relationship with `Owner` and a one-to-many relationship with `Visit`.
- **PetType**: Represents the type of pet (e.g., Cat, Dog). Attributes include name.
- **Visit**: Represents a veterinary visit. Attributes include date and description. Has a many-to-one relationship with `Pet`.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can find owners by last name prefix in under 3 seconds.
- **SC-002**: New owners can be created and their details displayed within 5 seconds of form submission.
- **SC-003**: The owner list page loads with pagination within 4 seconds, supporting up to 1000 concurrent users.
- **SC-004**: 95% of pet creation/update operations complete successfully with valid data.
- **SC-005**: 98% of visit bookings for existing pets are successful with valid dates.
- **SC-006**: Validation errors for owner and pet data are displayed to the user within 1 second of form submission.

## Assumptions

- Users have stable internet connectivity.
- The system will use a relational database for data persistence.
- Standard web browser functionality is assumed for user interaction.
- The application will be deployed in an environment where standard Spring Boot conventions are followed.
- Pet types (e.g., Cat, Dog) will be pre-populated or managed through a separate administrative interface not covered by this feature.
- The `owners` module is part of a larger Spring Petclinic application.
- Telephone numbers are expected to be in a 10-digit format for the specified region.