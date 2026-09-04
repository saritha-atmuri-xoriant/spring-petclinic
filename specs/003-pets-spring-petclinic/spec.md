# Feature Specification: Pet Management

**Feature Branch**: `003-pets-spring-petclinic`

**Created**: 2026-09-04

**Status**: Draft

**Input**: User description: "pets for spring-petclinic"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Add a new pet to an owner (Priority: P1)

As a clinic staff member, I want to add a new pet to an existing owner's record so that I can manage all their animals.

**Why this priority**: This is a core function for managing pet information and is essential for the application's primary purpose.

**Independent Test**: Can be fully tested by navigating to an owner's profile, initiating the "Add Pet" action, filling in valid pet details, and verifying the pet appears in the owner's list.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" exists, **When** I navigate to John Doe's profile and add a new pet named "Buddy" of type "Dog" with birth date "2023-01-15", **Then** "Buddy" appears in John Doe's pet list.
2. **Given** an owner "Jane Smith" exists, **When** I navigate to Jane Smith's profile and attempt to add a new pet without a name, **Then** an error message "Pet name must not be blank" is displayed, and the pet is not added.
3. **Given** an owner "Peter Jones" exists, **When** I navigate to Peter Jones's profile and attempt to add a new pet without selecting a type, **Then** an error message "Pet type must not be blank" is displayed, and the pet is not added.
4. **Given** an owner "Alice Brown" exists, **When** I navigate to Alice Brown's profile and attempt to add a new pet without a birth date, **Then** an error message "Pet birth date must not be blank" is displayed, and the pet is not added.

---

### User Story 2 - Update an existing pet's details (Priority: P2)

As a clinic staff member, I want to update an existing pet's information (like name or type) so that the records are accurate.

**Why this priority**: Maintaining accurate pet information is crucial for effective clinic operations.

**Independent Test**: Can be fully tested by selecting an existing pet, modifying its details, saving the changes, and verifying the updated information is displayed.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" has a pet named "Buddy" of type "Dog", **When** I edit "Buddy" to change its name to "Buddy Jr." and its type to "Golden Retriever", **Then** the pet's name is updated to "Buddy Jr." and its type to "Golden Retriever" in John Doe's pet list.
2. **Given** an owner "Jane Smith" has a pet named "Whiskers", **When** I attempt to update "Whiskers" to have a birth date in the future, **Then** an error message "Invalid birth date" is displayed, and the birth date is not updated.

---

### User Story 3 - Prevent duplicate pet names for the same owner (Priority: P3)

As a clinic staff member, I want to be prevented from adding a pet with a name that already exists for the same owner, to avoid confusion.

**Why this priority**: This ensures data integrity and prevents potential user errors.

**Independent Test**: Can be fully tested by adding a pet with a specific name to an owner, then attempting to add another pet with the exact same name to the same owner, and verifying the error message.

**Acceptance Scenarios**:

1. **Given** an owner "John Doe" has a pet named "Buddy", **When** I attempt to add another pet for "John Doe" named "Buddy", **Then** an error message "Pet name must be unique within an owner's pets" is displayed, and the second pet is not created.

---

### Edge Cases

- What happens when a pet's birth date is in the future? → System rejects with a "typeMismatch.birthDate" error.
- What happens when a visit is booked with a date in the past or today? → System rejects with a "typeMismatch.visitDate" error.
- What happens when a request is made for a pet or visit associated with a non-existent owner ID? → System throws an `IllegalArgumentException` indicating the owner was not found.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow the creation of a new pet for an existing owner.
- **FR-002**: System MUST validate that a pet's name is provided.
- **FR-003**: System MUST validate that a pet's type is provided if the pet is new.
- **FR-004**: System MUST validate that a pet's birth date is provided.
- **FR-005**: System MUST support the creation of pets with different types.
- **FR-006**: System MUST allow updating an existing pet's details.
- **FR-007**: System MUST enforce that a pet's name is unique within an owner's pets.
- **FR-008**: System MUST validate that an owner's telephone number contains exactly 10 digits.
- **FR-009**: System MUST validate that an owner's address is not blank.
- **FR-010**: System MUST validate that an owner's city is not blank.
- **FR-011**: System MUST validate that an owner's first name is not blank.
- **FR-012**: System MUST validate that an owner's last name is not blank.
- **FR-013**: System MUST validate that a pet type name is not blank.
- **FR-014**: System MUST validate that a specialty name is not blank.

### Key Entities *(include if feature involves data)*

- **Pet**: Represents an animal owned by a person. Attributes include birthDate and type. It has a relationship with PetType and Visit.
- **PetType**: Represents the category of a pet (e.g., Dog, Cat). Attributes include name.
- **Visit**: Represents a medical visit for a pet. Attributes include description and date. It is associated with a Pet.
- **Owner**: Represents the owner of pets. Attributes include address, city, and telephone. It has a OneToMany relationship with Pet.
- **Person**: Base class for individuals, including owners. Attributes include firstName and lastName.
- **NamedEntity**: Base class for entities with a name.
- **BaseEntity**: Base class for entities with an ID.
- **Vet**: Represents a veterinarian. Attributes include specialties.
- **Specialty**: Represents a veterinarian's area of expertise. Attributes include name.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can add a new pet to an owner's record in under 1 minute.
- **SC-002**: System prevents duplicate pet names for the same owner with an error message displayed within 2 seconds.
- **SC-003**: 95% of pet updates are successfully processed and reflected in the system within 3 seconds.
- **SC-004**: All validation errors for pet creation/update are displayed to the user clearly and immediately upon submission.

## Assumptions

- Users have stable internet connectivity.
- The application will be accessed via a web browser.
- Existing owner records are available for pet association.
- The set of available pet types and vet specialties are predefined and managed separately.
- Error messages will be user-friendly and informative.