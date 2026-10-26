# Feature: Maintain Ref

**Feature ID:** 9  
**Branch pattern:** `feature/9-maintain-ref`  
**Status:** Draft  
**Created:** 2026-10-21  
**Input:** Maintain referees, their availability, and their assignment to games.  
**Depends on:** [Feature 1-User-Authentication](Feature-1-User-Authentication.md),[Feature 5-Maintain-Game](Feature-5-Maintain-Game.md)

------

## User Stories

### US-9.1: Add ref

**As an** owner  
**I want to** add a ref  
**So that** I have a list of refs to schedule.  
**Priority:** P1  
**Independent test:** Add a ref and verify that the ref is saved.  
**Acceptance Scenarios:** see ### US-9.1 under Gherkin AC

### US-9.2: Edit ref

**As an** owner  
**I want to** edit a ref  
**So that** the ref information and pay rate stay accurate.  
**Priority:** P1  
**Independent test:** Edit a ref and verify that the change is saved.  
**Acceptance Scenarios:** see ### US-9.2 under Gherkin AC

### US-9.3: Delete ref

**As an** owner  
**I want to** delete a ref  
**So that** a ref who left can be removed.  
**Priority:** P1  
**Independent test:** Delete a ref and verify that the ref is no longer active.  
**Acceptance Scenarios:** see ### US-9.3 under Gherkin AC

### US-9.4: View refs

**As an** owner  
**I want to** view the refs with their games count  
**So that** I can share the work fairly.  
**Priority:** P1  
**Independent test:** Open the ref list and verify that the games count is shown.  
**Acceptance Scenarios:** see ### US-9.4 under Gherkin AC

### US-9.5: Set ref sports and availability

**As an** owner  
**I want to** set the sports and the available days and times of a ref  
**So that** I schedule refs only when they can come.  
**Priority:** P2  
**Independent test:** Set availability and verify that it is saved.  
**Acceptance Scenarios:** see ### US-9.5 under Gherkin AC

### US-9.6: Assign ref to game

**As an** owner  
**I want to** assign a ref to a game  
**So that** every game is covered.  
**Priority:** P1  
**Independent test:** Assign a ref and verify that the assignment is saved.  
**Acceptance Scenarios:** see ### US-9.6 under Gherkin AC

### US-9.7: Confirm or decline a game

**As a** ref  
**I want to** confirm or decline a game I am assigned to  
**So that** the owner knows if I will come.  
**Priority:** P1  
**Independent test:** Decline a game and verify that the owner sees it.  
**Acceptance Scenarios:** see ### US-9.7 under Gherkin AC

### US-9.8: View my schedule

**As a** ref  
**I want to** see my own game schedule with date, time and location  
**So that** I know where to go.  
**Priority:** P1  
**Independent test:** Log in as a ref and verify that only own games are shown.  
**Acceptance Scenarios:** see ### US-9.8 under Gherkin AC

-----

## Functional Requirements

- **FR-001:** The system MUST maintain refs.
- **FR-002:** Each ref MUST have a unique identifier.
- **FR-003:** The system MUST allow authorized users to add refs.
- **FR-004:** The system MUST allow authorized users to edit refs.
- **FR-005:** The system MUST allow authorized users to delete refs.
- **FR-006:** The system MUST allow authorized users to view refs.
- **FR-007:** Required ref information MUST be provided before the ref can be saved (name, email, phone, pay rate per game).
- **FR-008:** A ref MUST have a list of sports they can work and the days and times they are available.
- **FR-009:** The system MUST let the owner assign one or more refs to a game.
- **FR-010:** The system MUST warn the owner when a ref is not available, cannot work that sport, or already has a game at that time.
- **FR-011:** A game that has no confirmed ref MUST be shown as Needs ref until the owner fills it.
- **FR-012:** The system MUST warn the owner when a ref with future assignments is made inactive.
- **FR-013:** A ref MUST be able to confirm or decline an assignment. The owner MUST see the status (Pending, Confirmed, Declined).
- **FR-014:** The system MUST show the owner the number of games for each ref, the refs with no games, and the games without a ref.
- **FR-015:** The system MUST NOT delete a ref that has unpaid or future assignments.
- **FR-016:** Deleting a ref MUST be a soft delete (record state Deleted), so other features keep the original ref information.
- **FR-017:** A ref MUST be able to view only their own games.
- **FR-018:** Ref email and phone MUST NOT be shown on the public pages.
- **FR-019:** The system MUST let the owner use this feature (main user: owner), and MUST let a ref confirm or decline only their own assignments.
- **FR-020:** The system MUST work on an office computer and on a phone.

-----

## Screen Requirements

### SCR-9.1: Ref list page

- **Who can open it:** Owner only
- **Content:** A table of refs with these columns: Name, Email, Phone, Pay rate per game, Sports, Number of games, Record state
- **Fields:** Filter (All refs or Refs with no games)
- **Buttons and links:** Add ref, View, Edit, Set sports and availability, Delete, Make inactive / Make active, Games without a ref
- **Rules:**
  - Show the number of games for each ref (FR-014).
  - The owner can show only the refs with no games (FR-014).
  - Refs with the state Deleted are not shown in the list.
  - Other roles cannot open this page (FR-019).
- **Related:** US-9.4, FR-006, FR-014, FR-019

### SCR-9.2: Add ref page

- **Who can open it:** Owner only
- **Fields:** Name (required), Email (required), Phone (required), Pay rate per game (required), Sports (required, choose one or more sports)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - If a required field is empty, do not save and show which field is missing (FR-007).
  - A new ref starts with the state Active.
  - After saving, the owner can set the availability of the ref (SCR-9.4).
- **Related:** US-9.1, FR-003, FR-007, FR-008

### SCR-9.3: Edit ref page

- **Who can open it:** Owner only
- **Fields:** Name (required), Email (required), Phone (required), Pay rate per game (required), Record state (Active or Inactive)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - Show the current information of the ref when the page opens.
  - If a required field is removed, do not save the change (FR-007).
  - When the owner changes the state to Inactive and the ref has future assignments, show SCR-9.9 (FR-012).
- **Related:** US-9.2, FR-004, FR-007, FR-012

### SCR-9.4: Sports and availability page

- **Who can open it:** Owner only
- **Fields:** Sports (required, choose one or more sports), Available days and times (optional)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - Show the current sports and availability when the page opens.
  - A ref must have at least one sport (FR-008).
  - For example, the owner can set a ref available on weekends for basketball.
- **Related:** US-9.5, FR-008

### SCR-9.5: View ref page

- **Who can open it:** Owner only
- **Content:** Ref information (Name, Email, Phone, Pay rate, Record state), sports, availability, the number of games, and the list of assignments (game, date, time, status Pending, Confirmed or Declined)
- **Buttons and links:** Edit, Set sports and availability, Delete, Back to list
- **Rules:**
  - Show the information as read only.
  - Show the status of each assignment to the owner (FR-013).
- **Related:** US-9.4, US-9.5, FR-006, FR-013

### SCR-9.6: Games without a ref page

- **Who can open it:** Owner only
- **Content:** A table of the games that have no ref, and the games with no confirmed ref. Each game shows date, time, teams, location and ref status.
- **Buttons and links:** Assign ref, Back to ref list
- **Rules:**
  - Show the games without a ref (FR-014).
  - A game with no confirmed ref is shown as Needs ref until the owner fills it (FR-011).
  - When a ref declines a game, the game appears here as needing a new ref.
- **Related:** US-9.6, US-9.7, FR-011, FR-014

### SCR-9.7: Assign ref to game page

- **Who can open it:** Owner only
- **Fields:** Game (required), Ref (required, the owner can choose one or more refs)
- **Buttons and links:** Assign, Cancel
- **Rules:**
  - The owner can assign one or more refs to a game (FR-009).
  - Show a warning if the ref is not available on that day or time, cannot work that sport, or already has a game at that time (FR-010).
  - After saving, the assignment starts with the status Pending.
- **Related:** US-9.6, FR-009, FR-010, FR-013

### SCR-9.8: Delete confirm message

- **Who can open it:** Owner only (shown after the owner clicks Delete)
- **Content:** The ref name and a question such as "Do you want to delete this ref?"
- **Buttons and links:** Confirm delete, Cancel
- **Rules:**
  - If the ref has unpaid or future assignments, reject the delete and show a message. The ref and the assignments stay unchanged (FR-015).
  - If the ref has none, change the record state to Deleted (soft delete). Do not remove the data (FR-016).
- **Related:** US-9.3, FR-005, FR-015, FR-016

### SCR-9.9: Inactive ref warning message

- **Who can open it:** Owner only (shown when the owner makes a ref inactive and the ref has future assignments)
- **Content:** A warning with the number of future assignments of the ref
- **Buttons and links:** Make inactive, Open the assignments of this ref, Back
- **Rules:**
  - Show this message only when the ref has future assignments (FR-012).
- **Related:** FR-012

### SCR-9.10: My schedule page (ref)

- **Who can open it:** Ref only (login needed)
- **Content:** A table of the games assigned to the ref with these columns: Date, Time, Location, Teams, Assignment status (Pending, Confirmed, Declined)
- **Buttons and links:** Confirm, Decline (shown only for a Pending assignment)
- **Rules:**
  - A ref sees only their own games (FR-017).
  - A ref can confirm or decline only their own assignments. An action on another ref's game is rejected (FR-019).
  - After the ref confirms, the assignment shows Confirmed. After the ref declines, the owner sees the game as needing a new ref (FR-013).
- **Related:** US-9.7, US-9.8, FR-013, FR-017, FR-019

### Rules for all screens

- Every screen MUST work on an office computer and on a phone (FR-020).
- Only the owner can change ref information. A ref can only confirm or decline their own assignments. Other roles MUST be rejected (FR-019).
- The email and phone of a ref MUST NOT be shown on any public page (FR-018).
- Error messages MUST be short and clear.

-----

## Key Entities

- **Ref** — A referee who works games.
- **Ref assignment** — The link between one ref and one game.

-----

## Initial Data Model

### Ref

- ref_id: String — Required, unique
- name: String — Required
- email: String — Required
- phone: String — Required
- pay_rate: Decimal — Required, per game
- sports: List of Sport IDs — Required
- availability: List of days and times — Optional
- record_state: String — Required (Active, Inactive, Deleted). Deleted is a soft delete, see shared/GLOSSARY.md

### Ref assignment

- assignment_id: String — Required, unique
- game_id: String — Required
- ref_id: String — Required
- status: String — Required (Pending, Confirmed, Declined)

-----

## Gherkin AC

### US-9.1 — Add ref

#### Scenario: Ref is saved

- **Given** a ref does not already exist
- **When** the owner enters the required ref information and saves
- **Then** the system saves the ref

#### Scenario: Ref is not saved due to missing information

- **Given** a ref is being added
- **When** required ref information is missing
- **Then** the system does not save the ref

#### Scenario: Wrong role cannot change information

- **Given** a manager is signed in
- **When** the manager tries to change information in this feature
- **Then** the system rejects the change

### US-9.2 — Edit ref

#### Scenario: Ref is edited successfully

- **Given** a ref exists
- **When** the owner changes the ref information and saves
- **Then** the system saves the updated ref

#### Scenario: Ref edit fails

- **Given** a ref exists
- **When** required information is removed during edit
- **Then** the system does not save the update

### US-9.3 — Delete ref

#### Scenario: Ref is deleted successfully

- **Given** a ref exists and has no unpaid or future assignments
- **When** the owner deletes the ref
- **Then** the system removes the ref from active records

#### Scenario: Ref with assignments cannot be deleted

- **Given** a ref has future assignments
- **When** the owner tries to delete the ref
- **Then** the system rejects the delete operation
- **And** the ref and the assignments stay unchanged

#### Scenario: Delete unknown ref fails

- **Given** the ref does not exist
- **When** the owner tries to delete the ref
- **Then** the system rejects the delete operation

### US-9.4 — View refs

#### Scenario: Ref list is displayed

- **Given** refs exist
- **When** the owner opens the ref list
- **Then** the system shows each ref with the number of games

#### Scenario: Refs with no games are listed

- **Given** a ref has no games
- **When** the owner opens the list of refs with no games
- **Then** the system shows that ref

### US-9.5 — Set ref sports and availability

#### Scenario: Availability is saved

- **Given** a ref exists
- **When** the owner sets the ref available on weekends for basketball
- **Then** the system saves the sports and availability

### US-9.6 — Assign ref to game

#### Scenario: Ref is assigned

- **Given** a game has no ref
- **When** the owner assigns an available ref
- **Then** the system saves the assignment with the status Pending

#### Scenario: Ref has another game

- **Given** Paul has a game at 6 PM
- **When** the owner assigns Paul to another game at 6 PM
- **Then** the system warns that the ref already has a game at this time

#### Scenario: Ref is not available

- **Given** Paul is available only on weekends
- **When** the owner assigns Paul to a Tuesday game
- **Then** the system warns that the ref is not available on this day

#### Scenario: Games without a ref are listed

- **Given** 3 games have no ref
- **When** the owner opens the list of games without a ref
- **Then** the system shows those 3 games

#### Scenario: Game without a confirmed ref

- **Given** a game has only a Pending ref
- **When** the owner opens the game list
- **Then** the game is shown as Needs ref

### US-9.7 — Confirm or decline a game

#### Scenario: Ref confirms a game

- **Given** Paul has a Pending assignment
- **When** Paul confirms it
- **Then** the assignment shows Confirmed

#### Scenario: Ref declines a game

- **Given** Paul has a Pending assignment
- **When** Paul declines it
- **Then** the owner sees the game as needing a new ref

#### Scenario: Ref cannot answer for another ref

- **Given** Paul is signed in
- **When** Paul tries to confirm a game assigned to another ref
- **Then** the system rejects the action

### US-9.8 — View my schedule

#### Scenario: Ref sees only own games

- **Given** Paul is signed in
- **When** Paul opens the schedule
- **Then** the system shows only the games assigned to Paul
