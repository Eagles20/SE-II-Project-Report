# Feature: Ministry Children

**Feature ID:** 3

**Branch pattern:** `feature/3-ministry-children`

**Status:** Draft

**Created:** 2026-10-02

**Input:** Church staff can put children in ministry groups and link each child to a guardian.

**Depends on:** [Feature-1 user authentication and management](<Feature-1 user authentication and management.md>), [Feature-2 member management](<Feature-2 member management.md>)

---

## User Stories

### US-3.1: Create a ministry group
**As a** church admin

**I want to** create a children's ministry group with an age range

**So that** children are in groups by age.

**Priority:** P1

**Independent test:** The admin creates a group and it shows in the list of groups.

**Acceptance scenarios:** see ### US-3.1 under Gherkin AC

### US-3.2: Register a child
**As a** church admin

**I want to** register a child and link the child to a guardian who is a member

**So that** the church knows who is responsible for each child.

**Priority:** P1

**Independent test:** The admin registers a child with a guardian and the child shows in the children list.

**Acceptance scenarios:** see ### US-3.2 under Gherkin AC

### US-3.3: Put a child in a group
**As a** church admin

**I want to** put a child in a ministry group

**So that** the child is in the right class.

**Priority:** P1

**Independent test:** After this, the child shows in the class list of the group.

**Acceptance scenarios:** see ### US-3.3 under Gherkin AC

### US-3.4: See a class list
**As a** church admin

**I want to** see the children in a ministry group

**So that** teachers know who is in their class.

**Priority:** P1

**Independent test:** The admin opens a group and sees all its children.

**Acceptance scenarios:** see ### US-3.4 under Gherkin AC

### US-3.5: Edit or remove a child or group
**As a** church admin

**I want to** change a child's information, move a child to another group, or remove a child or a group

**So that** the records stay correct.

**Priority:** P2

**Independent test:** The admin moves a child to another group and both class lists change.

**Acceptance scenarios:** see ### US-3.5 under Gherkin AC

---

## Functional Requirements

- **FR-001**: System MUST let a logged-in user create a ministry group with a name and an age range.
- **FR-002**: System MUST NOT allow two groups with the same name.
- **FR-003**: System MUST let the user register a child with a first name, a last name, a date of birth and a guardian.
- **FR-004**: System MUST ask for the guardian to be an existing member (Feature 2).
- **FR-005**: System MUST NOT register a child without the required information.
- **FR-006**: System MUST let the user put a child in one ministry group.
- **FR-007**: System MUST show the class list of a group.
- **FR-008**: System MUST let the user edit a child and move the child to another group.
- **FR-009**: System MUST let the user remove a child or a group, after a confirmation.
- **FR-010**: System MUST NOT remove a group that has children until the children are moved or removed.
- **FR-011**: System MUST require a login (Feature 1) for all ministry actions.

---

## Initial Data Model

The system keeps two things:

- **Ministry groups:** name (must be different for each group), the youngest age, and the oldest age.
- **Children:** first name, last name and date of birth (required), a guardian (one member, required), and one ministry group (optional).

---

## Gherkin AC

### US-3.1 — Create a ministry group

#### Scenario: Create a group
* **Given** the admin is creating a group
* **When** the admin enters a new name and an age range and saves
* **Then** the system creates the group
* **And** the group shows in the list

#### Scenario: Same name
* **Given** a group with this name already exists
* **When** the admin creates another group with the same name
* **Then** the system does not create it
* **And** the system says the name is already used

### US-3.2 — Register a child

#### Scenario: Register a child
* **Given** the admin is registering a child
* **When** the admin enters the child's information and picks a member as guardian
* **Then** the system saves the child
* **And** the child shows in the children list

#### Scenario: Information missing
* **Given** the admin is registering a child
* **When** the admin saves without a required field or without a guardian
* **Then** the system does not create the child
* **And** the system shows what is missing

### US-3.3 — Put a child in a group

#### Scenario: Put a child in a group
* **Given** a child and a group exist
* **When** the admin puts the child in the group
* **Then** the child shows in the class list of the group

#### Scenario: Child is already in a group
* **Given** the child is in a group
* **When** the admin puts the child in another group
* **Then** the system moves the child
* **And** the child is not in the old class list anymore

### US-3.4 — See a class list

#### Scenario: See a class list
* **Given** a group has children
* **When** the admin opens the group
* **Then** the system shows each child's name and guardian

#### Scenario: Empty group
* **Given** a group has no children
* **When** the admin opens the group
* **Then** the system says the group is empty

### US-3.5 — Edit or remove a child or group

#### Scenario: Edit a child
* **Given** the admin is looking at a child
* **When** the admin changes the information and saves
* **Then** the system keeps the new information

#### Scenario: Remove a child
* **Given** the admin is looking at a child
* **When** the admin clicks remove and confirms
* **Then** the system removes the child
* **And** the child is not in any class list

#### Scenario: Remove a group with children
* **Given** a group has children
* **When** the admin tries to remove the group
* **Then** the system does not remove it
* **And** the system says to move or remove the children first
