# Feature: Member Management
**Feature ID:** 2
**Branch pattern:** `feature/2-member-management`
**Status:** Draft
**Created:** 2026-10-02
**Input:** Church staff can add members and keep their information in the church member system.
**Depends on:** [Feature-1 user authentication and management](<Feature-1 user authentication and management.md>)

---

## User Stories

### US-2.1: Register a new member
**As a** church admin
**I want to** register a new member
**So that** the church has a clear list of its members.

**Priority:** P1
**Independent test:** The admin enters the member's information and saves the member.
**Acceptance scenarios:** see ### US-2.1 under Gherkin AC

### US-2.2: Save member information
**As a** church admin
**I want to** save a member's information
**So that** I can see and manage it later.

**Priority:** P1
**Independent test:** After registering a member, the admin can find the member and see the saved information.
**Acceptance scenarios:** see ### US-2.2 under Gherkin AC

### US-2.3: View and search members
**As a** church admin
**I want to** see the list of members, search by name, and open a member's details
**So that** I can find information quickly.

**Priority:** P1
**Independent test:** The admin searches for a member by name and opens the details.
**Acceptance scenarios:** see ### US-2.3 under Gherkin AC

### US-2.4: Edit member information
**As a** church admin
**I want to** change a member's information
**So that** the records stay correct.

**Priority:** P2
**Independent test:** The admin changes a phone number, saves, and sees the new number.
**Acceptance scenarios:** see ### US-2.4 under Gherkin AC

### US-2.5: Delete a member
**As a** church admin
**I want to** delete a member
**So that** people who are not members anymore are removed from the list.

**Priority:** P2
**Independent test:** The admin deletes a member and the member is not in the list anymore.
**Acceptance scenarios:** see ### US-2.5 under Gherkin AC

---

## Functional Requirements

- **FR-001**: System MUST let a logged-in user add a new member.
- **FR-002**: System MUST ask for the first name and the last name of the member.
- **FR-003**: System MUST NOT register a member without the required information.
- **FR-004**: System MUST NOT create a second record for a member who already exists.
- **FR-005**: System MUST save the member's information after registration.
- **FR-006**: System MUST show the list of members and the details of one member.
- **FR-007**: System MUST let the user search members by name.
- **FR-008**: System MUST let the user edit a member, with the same checks as registration.
- **FR-009**: System MUST let the user delete a member, after a confirmation.
- **FR-010**: System MUST NOT delete a member who is a guardian of a child, a driver of a route, or a preacher of a service, until that link is removed.
- **FR-011**: System MUST require a login (Feature 1) for all member actions.

---

## Initial Data Model

The system keeps one thing:

- **Members:** first name and last name (required), phone, email and address (optional).


---

## Gherkin AC

### US-2.1 — Register a new member

#### Scenario: Register a member
* **Given** the admin is registering a new member
* **When** the admin enters all the required information and saves
* **Then** the system saves the member
* **And** the member shows in the member list

#### Scenario: Information missing
* **Given** the admin is registering a new member
* **When** the admin saves without the required information
* **Then** the system does not create the member
* **And** the system shows what is missing

### US-2.2 — Save member information

#### Scenario: Information is saved
* **Given** the admin entered correct information
* **When** the admin saves the member
* **Then** the system keeps the information
* **And** the admin can see it later

#### Scenario: Member already exists
* **Given** the member already exists
* **When** the admin tries to register the same member again
* **Then** the system does not create a second record
* **And** the system says the member already exists

### US-2.3 — View and search members

#### Scenario: See the list
* **Given** members exist
* **When** the admin opens the member list
* **Then** the system shows the members

#### Scenario: Search by name
* **Given** the admin is looking at the member list
* **When** the admin searches by a name
* **Then** the system shows only the members that match

#### Scenario: See the details
* **Given** the admin is looking at the member list
* **When** the admin clicks a member
* **Then** the system shows the member's information

### US-2.4 — Edit member information

#### Scenario: Edit a member
* **Given** the admin is looking at a member
* **When** the admin changes the information and saves
* **Then** the system keeps the new information

#### Scenario: Required field cleared
* **Given** the admin is editing a member
* **When** the admin clears a required field and saves
* **Then** the system does not save the change
* **And** the system shows what is missing

### US-2.5 — Delete a member

#### Scenario: Delete a member
* **Given** the admin is looking at a member
* **When** the admin clicks delete and confirms
* **Then** the system deletes the member
* **And** the member is not in the list anymore

#### Scenario: Cancel the delete
* **Given** the admin is asked to confirm
* **When** the admin clicks cancel
* **Then** the member stays the same

#### Scenario: Member is linked
* **Given** the member is a guardian, a driver or a preacher
* **When** the admin tries to delete the member
* **Then** the system does not delete the member
* **And** the system says which link to remove first
