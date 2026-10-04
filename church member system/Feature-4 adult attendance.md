# Feature: Adult Attendance

**Feature ID:** 4
**Branch pattern:** `feature/4-adult-attendance`
**Status:** Draft
**Created:** 2026-10-02
**Input:** Church staff can record which adult members came to each service.
**Depends on:** [Feature-1 user authentication and management](<Feature-1 user authentication and management.md>), [Feature-2 member management](<Feature-2 member management.md>)

---

## User Stories

### US-4.1: Choose a service
**As a** church admin
**I want to** choose a service from the list
**So that** I can record attendance for it.

**Priority:** P1
**Independent test:** The admin opens the list of services, chooses one, and sees its attendance page.
**Acceptance scenarios:** see ### US-4.1 under Gherkin AC

### US-4.2: Mark an adult present
**As a** church admin
**I want to** mark an adult member as present for a service
**So that** the church knows who came.

**Priority:** P1
**Independent test:** The admin marks a member present and the member shows in the attendance list.
**Acceptance scenarios:** see ### US-4.2 under Gherkin AC

### US-4.3: See the attendance of a service
**As a** church admin
**I want to** see who came to a service and how many
**So that** I can make a report.

**Priority:** P1
**Independent test:** The admin opens a service and sees the list and the total.
**Acceptance scenarios:** see ### US-4.3 under Gherkin AC

### US-4.4: Fix an attendance mistake
**As a** church admin
**I want to** remove a wrong attendance entry
**So that** the records stay correct.

**Priority:** P2
**Independent test:** The admin removes an entry and the member is not in the list anymore.
**Acceptance scenarios:** see ### US-4.4 under Gherkin AC

### US-4.5: See a member's attendance history
**As a** church admin
**I want to** see the services a member came to
**So that** I can follow up with members who are often absent.

**Priority:** P3
**Independent test:** The admin opens a member and sees the services the member came to.
**Acceptance scenarios:** see ### US-4.5 under Gherkin AC

---

## Functional Requirements

- **FR-001**: System MUST let a logged-in user choose an existing service (made in Feature 1) to record attendance.
- **FR-002**: System MUST let the user mark an existing member as present for a service.
- **FR-003**: System MUST NOT record the same member twice for the same service.
- **FR-004**: System MUST show the list of people who came and the total for a service.
- **FR-005**: System MUST let the user remove an attendance entry.
- **FR-006**: System MUST let the user see the attendance history of a member.
- **FR-007**: System MUST require a login (Feature 1) for all attendance actions.

---

## Initial Data Model

 The system keeps one more thing:

- **Adult attendance:** which service, which member, and when it was saved. A member can be saved only once for each service.

---

## Gherkin AC

### US-4.1 — Choose a service

#### Scenario: Choose a service
* **Given** services exist
* **When** the admin chooses a service from the list
* **Then** the system opens the attendance page of the service

#### Scenario: No services yet
* **Given** there are no services
* **When** the admin opens the list of services
* **Then** the system says to create a service first

### US-4.2 — Mark an adult present

#### Scenario: Mark a member present
* **Given** a service and a member exist
* **When** the admin marks the member present
* **Then** the system saves the attendance
* **And** the member shows in the attendance list

#### Scenario: Already marked
* **Given** the member is already marked present
* **When** the admin marks the same member again
* **Then** the system does not add a second entry
* **And** the system says the member is already marked

### US-4.3 — See the attendance of a service

#### Scenario: See the attendance
* **Given** attendance is saved for a service
* **When** the admin opens the service
* **Then** the system shows the people who came
* **And** the system shows the total

#### Scenario: No attendance yet
* **Given** no attendance is saved for a service
* **When** the admin opens the service
* **Then** the system shows a total of zero

### US-4.4 — Fix an attendance mistake

#### Scenario: Remove an entry
* **Given** a member is marked present
* **When** the admin removes the entry and confirms
* **Then** the member is not in the list anymore
* **And** the total goes down by one

### US-4.5 — See a member's attendance history

#### Scenario: See the history
* **Given** a member came to several services
* **When** the admin opens the member's history
* **Then** the system shows each service, newest first
