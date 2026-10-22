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
