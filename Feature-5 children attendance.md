# Feature: Children Attendance

**Feature ID:** 5

**Branch pattern:** `feature/5-children-attendance`

**Status:** Draft

**Created:** 2026-10-02

**Input:** Church staff can record which children came to each service, by ministry group.

**Depends on:** [Feature-1 user authentication and management](<Feature-1 user authentication and management.md>), [Feature-3 ministry children](<Feature-3 ministry children.md>)

---

## User Stories

### US-5.1: Check in a child
**As a** children's ministry teacher

**I want to** check in a child for a service

**So that** the church knows which children are here.

**Priority:** P1

**Independent test:** The teacher checks in a child and the child shows in the list of the service.

**Acceptance scenarios:** see ### US-5.1 under Gherkin AC

### US-5.2: See attendance by group
**As a** children's ministry teacher

**I want to** see which children of my group are here

**So that** I know who I am responsible for.

**Priority:** P1

**Independent test:** The teacher opens a group for a service and sees who is here and who is not.

**Acceptance scenarios:** see ### US-5.2 under Gherkin AC

### US-5.3: Fix a check-in mistake
**As a** church admin

**I want to** remove a wrong check-in

**So that** the records stay correct.

**Priority:** P2

**Independent test:** The admin removes a check-in and the child is not shown as here anymore.

**Acceptance scenarios:** see ### US-5.3 under Gherkin AC

### US-5.4: See a child's attendance history
**As a** church admin

**I want to** see the services a child came to

**So that** I can share it with the guardian or follow up.

**Priority:** P3

**Independent test:** The admin opens a child and sees the services the child came to.

**Acceptance scenarios:** see ### US-5.4 under Gherkin AC

---

## Functional Requirements

- **FR-001**: System MUST let a logged-in user check in a registered child for an existing service.
- **FR-002**: System MUST NOT check in the same child twice for the same service.
- **FR-003**: System MUST save the group of the child at the time of check-in.
- **FR-004**: System MUST show, for a service, which children of a group are here and which are not.
- **FR-005**: System MUST show how many children are here.
- **FR-006**: System MUST let the user remove a check-in.
- **FR-007**: System MUST let the user see the attendance history of a child.
- **FR-008**: System MUST require a login (Feature 1) for all children attendance actions.

---

## Initial Data Model

Services come from Feature 1 and children come from Feature 3. The system keeps one more thing:

- **Children attendance:** which service, which child, the child's group at check-in, and the check-in time. A child can be checked in only once for each service.

---

## Gherkin AC

### US-5.1 — Check in a child

#### Scenario: Check in a child
* **Given** a service and a registered child exist
* **When** the teacher checks in the child
* **Then** the system saves the check-in
* **And** the child shows in the list of the service

#### Scenario: Already checked in
* **Given** the child is already checked in
* **When** the teacher checks in the same child again
* **Then** the system does not add a second entry
* **And** the system says the child is already checked in

### US-5.2 — See attendance by group

#### Scenario: See a group
* **Given** a group has children and some are checked in
* **When** the teacher opens the group for the service
* **Then** the system shows who is here and who is not
* **And** the system shows how many are here

### US-5.3 — Fix a check-in mistake

#### Scenario: Remove a check-in
* **Given** a child is checked in
* **When** the admin removes the check-in and confirms
* **Then** the child is not shown as here anymore
* **And** the number of children here goes down by one

### US-5.4 — See a child's attendance history

#### Scenario: See the history
* **Given** a child came to several services
* **When** the admin opens the child's history
* **Then** the system shows each service, newest first
