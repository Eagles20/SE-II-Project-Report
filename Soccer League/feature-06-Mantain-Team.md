# Feature: Maintain Team

**Feature ID:** 6  
**Branch pattern:** `feature/6-maintain-team`  
**Status:** Draft  
**Created:** 2026-10-20  
**Input:** Maintain teams, their managers and home locations in a league.  
**Depends on:** [Feature 3 -Maintain-League](Feature-3-Maintain-League.md), [Feature 8-Maintain-Location](Feature8-Maintain-Location.md)

------

## User Stories

### US-6.1: Add team

**As an** owner  
**I want to** add a team to a league  
**So that** it can play in the season.  
**Priority:** P1  
**Independent test:** Add a team and verify that it is saved.  
**Acceptance Scenarios:** see ### US-6.1 under Gherkin AC

### US-6.2: Edit team

**As an** owner  
**I want to** edit a team  
**So that** the team information stays accurate.  
**Priority:** P1  
**Independent test:** Edit a team and verify that the change is saved.  
**Acceptance Scenarios:** see ### US-6.2 under Gherkin AC

### US-6.3: Delete team

**As an** owner  
**I want to** delete a team  
**So that** a team made by mistake can be removed.  
**Priority:** P1  
**Independent test:** Delete a team and verify that it is no longer active.  
**Acceptance Scenarios:** see ### US-6.3 under Gherkin AC

### US-6.4: View team

**As a** manager  
**I want to** view my team with its roster, games and record  
**So that** I know where my team stands.  
**Priority:** P1  
**Independent test:** Open a team and verify that its roster, games and record are displayed.  
**Acceptance Scenarios:** see ### US-6.4 under Gherkin AC

### US-6.5: Change team manager

**As an** owner  
**I want to** change the manager of a team  
**So that** I can replace a manager who leaves.  
**Priority:** P2  
**Independent test:** Change a manager and verify the access change.  
**Acceptance Scenarios:** see ### US-6.5 under Gherkin AC

### US-6.6: Make team inactive

**As an** owner  
**I want to** make a team inactive  
**So that** it stops appearing in new schedules but keeps its history.  
**Priority:** P2  
**Independent test:** Make a team inactive and verify that the schedule generator skips it.  
**Acceptance Scenarios:** see ### US-6.6 under Gherkin AC

### US-6.7: Check team problems

**As an** owner  
**I want to** see teams with no manager or too few players  
**So that** I can fix them before the season starts.  
**Priority:** P2  
**Independent test:** Open the team list and verify that the warnings are shown.  
**Acceptance Scenarios:** see ### US-6.7 under Gherkin AC

### US-6.8: Public views teams

**As a** person from the public  
**I want to** open a team page and search teams by name  
**So that** I can follow my team.  
**Priority:** P2  
**Independent test:** Open a public team page and verify that players, games and record are shown.  
**Acceptance Scenarios:** see ### US-6.8 under Gherkin AC

-----

## Functional Requirements

- **FR-001:** The system MUST maintain teams.
- **FR-002:** Each team MUST have a unique identifier.
- **FR-003:** The system MUST allow authorized users to add teams.
- **FR-004:** The system MUST allow authorized users to edit teams.
- **FR-005:** The system MUST allow authorized users to delete teams.
- **FR-006:** The system MUST allow authorized users to view teams.
- **FR-007:** Required team information MUST be provided before the team can be saved (name, league, manager).
- **FR-008:** A team name MUST be unique inside its league.
- **FR-009:** Every team MUST belong to one league and have one manager.
- **FR-010:** The system MUST let the owner change the manager of a team. The old manager MUST lose access to that team.
- **FR-011:** A manager MUST be able to edit only their own team.
- **FR-012:** The system MUST NOT delete a team that has games.
- **FR-013:** Deleting a team MUST be a soft delete (record state Deleted), so other features keep the original team information.
- **FR-014:** A team MUST have a record state (Active, Inactive or Deleted. Inactive teams MUST NOT be used when games are generated.
- **FR-015:** The system MUST warn the owner when a team with future games is made inactive.
- **FR-016:** The system MUST warn the owner when a team has fewer players than the league minimum or has no manager.
- **FR-017:** The system MUST calculate the team record (wins, losses, ties) from the game results.
- **FR-018:** The system MUST let the owner and the managers use this feature (main user: owner), and MUST NOT let other roles change its information.
- **FR-019:** The system MUST work on an office computer and on a phone.

-----

## Screen Requirements

### SCR-6.1: Team list page

- **Who can open it:** Owner only
- **Content:** A table of teams with these columns: Name, League, Manager, Home location, Number of players, Record state, Warnings
- **Buttons and links:** Add team, View, Edit, Change manager, Make inactive / Make active, Delete
- **Rules:**
  - Show a warning for a team that has no manager or has fewer players than the league minimum (FR-016).
  - Teams with the state Deleted are not shown in the list.
  - Other roles cannot open this page. A manager uses SCR-6.7 to see their own team (FR-018).
- **Related:** US-6.6, US-6.7, FR-006, FR-016, FR-018

### SCR-6.2: Add team page

- **Who can open it:** Owner only
- **Fields:** League (required), Name (required), Manager (required, choose a user), Home location (optional)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - If a required field is empty, do not save and show which field is missing (FR-007).
  - Reject a team name that already exists in the same league (FR-008).
  - Every team has one league and one manager (FR-009).
  - A new team starts with the state Active.
- **Related:** US-6.1, FR-003, FR-007, FR-008, FR-009

### SCR-6.3: Edit team page

- **Who can open it:** Owner, and a manager for their own team only
- **Fields:** Name (required), Home location (optional). The owner also sees League (required) and Record state (Active or Inactive).
- **Buttons and links:** Save, Cancel
- **Rules:**
  - Show the current information of the team when the page opens.
  - If a required field is removed, do not save the change (FR-007).
  - Reject a team name that already exists in the same league (FR-008).
  - A manager can edit only their own team. A manager who opens another team is rejected (FR-011).
  - Only the owner can change the manager. Use SCR-6.4 for this (FR-010).
  - When the owner changes the state to Inactive and the team has future games, show SCR-6.5 (FR-015).
- **Related:** US-6.2, US-6.6, FR-004, FR-008, FR-011, FR-014, FR-015

### SCR-6.4: Change manager page

- **Who can open it:** Owner only
- **Fields:** New manager (required, choose a user)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - Show the current manager when the page opens.
  - After saving, the new manager can manage the team and the old manager loses access to that team (FR-010).
- **Related:** US-6.5, FR-010

### SCR-6.5: Inactive team warning message

- **Who can open it:** Owner only (shown when the owner makes a team inactive and the team has future games)
- **Content:** A warning with the number of future games of the team, and a request to move or cancel them
- **Buttons and links:** Make inactive, Open the games of this team, Back
- **Rules:**
  - Show this message only when the team has future games (FR-015).
  - An inactive team is not used when games are generated (FR-014).
  - The team and its history stay in the system.
- **Related:** US-6.6, FR-014, FR-015

### SCR-6.6: Delete confirm message

- **Who can open it:** Owner only (shown after the owner clicks Delete)
- **Content:** The team name and a question such as "Do you want to delete this team?"
- **Buttons and links:** Confirm delete, Cancel
- **Rules:**
  - If the team has games, reject the delete and show a message. The team and its games stay unchanged (FR-012).
  - If the team has no games, change the record state to Deleted (soft delete). Do not remove the data (FR-013).
  - Past records keep showing the original team information (FR-013).
- **Related:** US-6.3, FR-005, FR-012, FR-013

### SCR-6.7: View team page

- **Who can open it:** Owner, and a manager for their own team
- **Content:** Team information (Name, League, Manager, Home location, Record state), the roster, the games, and the record (wins, losses, ties)
- **Buttons and links:** Edit, Back to list (owner only). The owner also sees Change manager and Delete.
- **Rules:**
  - Calculate the record from the game results (FR-017).
  - For example, a team that won 3 games and lost 1 shows 3 wins and 1 loss.
  - Show a warning when the team has fewer players than the league minimum or has no manager (FR-016).
  - A manager sees only their own team (FR-011).
- **Related:** US-6.4, US-6.7, FR-006, FR-016, FR-017

### SCR-6.8: Public team search page

- **Who can open it:** Everyone (no login needed)
- **Fields:** Search box (search by team name)
- **Content:** A list of matching teams
- **Buttons and links:** Open a team
- **Rules:**
  - Search finds teams by part of the name.
  - Show only teams with the state Active.
  - Do not show any edit buttons.
  - Do not ask for login.
- **Related:** US-6.8

### SCR-6.9: Public team page

- **Who can open it:** Everyone (no login needed)
- **Content:** The team name, league, players, games and record (wins, losses, ties)
- **Buttons and links:** Back to search
- **Rules:**
  - Do not show any edit buttons.
  - Do not show a team with the state Deleted.
- **Related:** US-6.8, FR-017

### Rules for all screens

- Every screen MUST work on an office computer and on a phone (FR-019).
- Only the owner and the managers can change information, and a manager only for their own team. Other roles MUST be rejected (FR-018).
- Error messages MUST be short and clear.

-----

## Key Entities

- **Team** — A group of players with one manager that plays in a league.

-----

## Initial Data Model

### Team

- team_id: String — Required, unique
- league_id: String — Required
- name: String — Required, unique in the league
- manager_user_id: String — Required
- home_location_id: String — Optional
- record_state: String — Required (Active, Inactive, Deleted). Deleted is a soft delete, see shared/GLOSSARY.md

-----

## Gherkin AC

### US-6.1 — Add team

#### Scenario: Team is saved

- **Given** a team does not already exist
- **When** the owner enters the required team information and saves
- **Then** the system saves the team

#### Scenario: Team is not saved due to missing information

- **Given** a team is being added
- **When** required team information is missing
- **Then** the system does not save the team

#### Scenario: Duplicate team name is rejected

- **Given** "Eagles" exists in "Fall League"
- **When** the owner adds another "Eagles" in "Fall League"
- **Then** the system rejects the duplicate team

#### Scenario: Wrong role cannot change information

- **Given** a ref is signed in
- **When** the ref tries to change information in this feature
- **Then** the system rejects the change

### US-6.2 — Edit team

#### Scenario: Team is edited successfully

- **Given** a team exists
- **When** the owner changes the team information and saves
- **Then** the system saves the updated team

#### Scenario: Manager edits own team

- **Given** a manager of "Eagles" is signed in
- **When** the manager changes the team name and saves
- **Then** the system saves the new name

#### Scenario: Manager cannot edit another team

- **Given** a manager of "Eagles" is signed in
- **When** the manager tries to edit "Hawks"
- **Then** the system rejects the change

### US-6.3 — Delete team

#### Scenario: Team is deleted successfully

- **Given** a team exists and has no games
- **When** the owner deletes the team
- **Then** the system removes the team from active records

#### Scenario: Team with games cannot be deleted

- **Given** a team has games
- **When** the owner tries to delete it
- **Then** the system rejects the delete operation
- **And** the team and its games stay unchanged

#### Scenario: Deleted team does not change past records

- **Given** a team was deleted and past records refer to it
- **When** someone views those past records
- **Then** the system still shows the original team information

#### Scenario: Delete unknown team fails

- **Given** the team does not exist
- **When** the owner tries to delete it
- **Then** the system rejects the delete operation

### US-6.4 — View team

#### Scenario: Team information is displayed

- **Given** a team exists
- **When** the manager views the team
- **Then** the system displays the roster, the games and the record

#### Scenario: Team record is calculated

- **Given** "Eagles" won 3 games and lost 1
- **When** someone views the team
- **Then** the record shows 3 wins and 1 loss

### US-6.5 — Change team manager

#### Scenario: Manager is changed

- **Given** "Sam" manages "Eagles"
- **When** the owner changes the manager to "Ben"
- **Then** Ben can manage "Eagles"
- **And** Sam can no longer manage "Eagles"

### US-6.6 — Make team inactive

#### Scenario: Inactive team is not scheduled

- **Given** "Hawks" is inactive
- **When** the owner generates the schedule
- **Then** "Hawks" has no new games

#### Scenario: Inactive team has future games

- **Given** "Hawks" has 3 future games
- **When** the owner makes "Hawks" inactive
- **Then** the system warns about the 3 games and asks the owner to move or cancel them

### US-6.7 — Check team problems

#### Scenario: Team has too few players

- **Given** the league minimum is 8 players and "Eagles" has 5 players
- **When** the owner opens the team
- **Then** the system warns that the team has fewer players than the minimum

#### Scenario: Team has no manager

- **Given** a team has no manager
- **When** the owner opens the team list
- **Then** the system shows the team in the list of teams without a manager

### US-6.8 — Public views teams

#### Scenario: Public sees a team page

- **Given** a team exists
- **When** a person who is not logged in opens the team page
- **Then** the system shows the players, the games and the record

#### Scenario: Public searches a team

- **Given** teams exist
- **When** a person searches for part of a team name
- **Then** the system shows the matching teams
