# Feature: Maintain League

**Feature ID:** 3  
**Branch pattern:** `feature/3-maintain-league`  
**Status:** Draft  
**Created:** 2026-10-21  
**Input:** Maintain leagues under a sport.  
**Depends on:** [Feature 2 — Maintain-Sport](feature-2-Maintain-Sport.md)

------

## User Stories

### US-3.1: Add league

**As an** owner  
**I want to** add a league under a sport  
**So that** teams can join it.  
**Priority:** P1  
**Independent test:** Add a league and verify that it is saved.  
**Acceptance Scenarios:** see ### US-3.1 under Gherkin AC

### US-3.2: Edit league

**As an** owner  
**I want to** edit a league  
**So that** the league information stays accurate.  
**Priority:** P1  
**Independent test:** Edit a league and verify that the change is saved.  
**Acceptance Scenarios:** see ### US-3.2 under Gherkin AC

### US-3.3: Delete league

**As an** owner  
**I want to** delete a league  
**So that** a league made by mistake can be removed.  
**Priority:** P1  
**Independent test:** Delete a league and verify that it is no longer active.  
**Acceptance Scenarios:** see ### US-3.3 under Gherkin AC

### US-3.4: View league

**As an** owner  
**I want to** open a league and see its teams and seasons  
**So that** I can understand its status in one place.  
**Priority:** P1  
**Independent test:** Open a league and verify that its teams and seasons are displayed.  
**Acceptance Scenarios:** see ### US-3.4 under Gherkin AC

### US-3.5: Set league rules

**As an** owner  
**I want to** set the number of games per team and the minimum and maximum players  
**So that** the schedule generator and the rosters follow the rules.  
**Priority:** P1  
**Independent test:** Set the rules and verify that they are saved and shown.  
**Acceptance Scenarios:** see ### US-3.5 under Gherkin AC

### US-3.6: Copy league

**As an** owner  
**I want to** copy the settings of a league into a new league  
**So that** I do not enter the same settings again each season.  
**Priority:** P3  
**Independent test:** Copy a league and verify that the settings are copied without teams.  
**Acceptance Scenarios:** see ### US-3.6 under Gherkin AC

### US-3.7: Make league inactive

**As an** owner  
**I want to** make a league inactive  
**So that** old records stay but the league is hidden from the public.  
**Priority:** P2  
**Independent test:** Make a league inactive and verify that the public cannot see it.  
**Acceptance Scenarios:** see ### US-3.7 under Gherkin AC

### US-3.8: Filter leagues by sport

**As an** owner  
**I want to** filter leagues by sport  
**So that** I can find the league I need.  
**Priority:** P3  
**Independent test:** Filter by a sport and verify that only its leagues are shown.  
**Acceptance Scenarios:** see ### US-3.8 under Gherkin AC

### US-3.9: Public views leagues

**As a** person from the public  
**I want to** browse leagues by sport and open a league page  
**So that** I can follow the league.  
**Priority:** P2  
**Independent test:** Open a public league page and verify seasons and teams are shown.  
**Acceptance Scenarios:** see ### US-3.9 under Gherkin AC

-----

## Functional Requirements

- **FR-001:** The system MUST maintain leagues.
- **FR-002:** Each league MUST have a unique identifier.
- **FR-003:** The system MUST allow authorized users to add leagues.
- **FR-004:** The system MUST allow authorized users to edit leagues.
- **FR-005:** The system MUST allow authorized users to delete leagues.
- **FR-006:** The system MUST allow authorized users to view leagues.
- **FR-007:** Required league information MUST be provided before the league can be saved (name, sport, games per team).
- **FR-008:** Every league MUST belong to one sport.
- **FR-009:** A league name MUST be unique inside the same sport.
- **FR-010:** A league MUST have a minimum and a maximum number of players per team.
- **FR-011:** The system MUST NOT delete a league that has teams or seasons.
- **FR-012:** Deleting a league MUST be a soft delete (record state Deleted), so other features keep the original league information.
- **FR-013:** A league MUST have a record state (Active, Inactive or Deleted, see shared/GLOSSARY.md). Inactive leagues MUST be hidden from the public but all data MUST stay.
- **FR-014:** The system MUST let the owner copy a league. The copy MUST keep the settings but MUST NOT copy teams, seasons or games.
- **FR-015:** The system MUST let the owner filter leagues by sport.
- **FR-016:** The system MUST let the owner use this feature (main user: owner), and MUST NOT let other roles change its information.
- **FR-017:** The system MUST work on an office computer and on a phone.
- **FR-018:** This feature is not used very often, so the system MUST ask the user to confirm before saving a change.

-----

## Screen Requirements

### SCR-3.1: League list page

- **Who can open it:** Owner only
- **Content:** A table of leagues with these columns: Name, Sport, Games per team, Players (min to max), Record state
- **Fields:** Sport filter (choose a sport or All sports)
- **Buttons and links:** Add league, View, Edit, Copy, Delete, Make inactive / Make active
- **Rules:**
  - When the owner chooses a sport, show only the leagues of that sport (FR-015).
  - Leagues with the state Deleted are not shown in the list.
  - Other roles cannot open this page (FR-016).
- **Related:** US-3.4, US-3.7, US-3.8, FR-006, FR-015, FR-016

### SCR-3.2: Add league page

- **Who can open it:** Owner only
- **Fields:** Sport (required), Name (required), Games per team (required), Minimum players (required), Maximum players (required), Description (optional)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - If a required field is empty, do not save and show which field is missing (FR-007, FR-010).
  - Games per team must be more than 0.
  - Minimum players must not be higher than maximum players.
  - Reject a league name that already exists in the same sport (FR-009).
  - When the owner clicks Save, show a confirm message before saving (FR-018).
  - A new league starts with the state Active.
- **Related:** US-3.1, US-3.5, FR-003, FR-007, FR-008, FR-009, FR-010, FR-018

### SCR-3.3: Edit league page

- **Who can open it:** Owner only
- **Fields:** Sport (required), Name (required), Games per team (required), Minimum players (required), Maximum players (required), Description (optional), Record state (Active or Inactive)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - Show the current information of the league when the page opens.
  - If a required field is removed, do not save the change (FR-007).
  - Minimum players must not be higher than maximum players.
  - Games per team must be more than 0.
  - Reject a league name that already exists in the same sport (FR-009).
  - When the owner clicks Save, show a confirm message before saving (FR-018).
  - Making a league Inactive hides it from the public. Seasons, games and stats stay (FR-013).
- **Related:** US-3.2, US-3.5, US-3.7, FR-004, FR-013, FR-018

### SCR-3.4: View league page

- **Who can open it:** Owner only
- **Content:** League information (Sport, Name, Games per team, Minimum and maximum players, Description, Record state), a list of teams, a list of seasons
- **Buttons and links:** Edit, Copy, Delete, Back to list
- **Rules:**
  - Show the league information as read only.
  - Show the teams and seasons of the league in one place.
- **Related:** US-3.4, FR-006

### SCR-3.5: Copy league page

- **Who can open it:** Owner only
- **Fields:** New league name (required), Sport (starts with the sport of the copied league)
- **Buttons and links:** Create copy, Cancel
- **Rules:**
  - Show the settings that will be copied: Games per team, Minimum and maximum players, Description.
  - The copy keeps the settings but does not copy teams, seasons or games (FR-014).
  - Reject a league name that already exists in the same sport (FR-009).
  - When the owner clicks Create copy, show a confirm message before saving (FR-018).
- **Related:** US-3.6, FR-009, FR-014, FR-018

### SCR-3.6: Delete confirm message

- **Who can open it:** Owner only (shown after the owner clicks Delete)
- **Content:** The league name and a question such as "Do you want to delete this league?"
- **Buttons and links:** Confirm delete, Cancel
- **Rules:**
  - If the league has teams or seasons, reject the delete and show a message. The league and the other records stay unchanged (FR-011).
  - If the league has no teams or seasons, change the record state to Deleted (soft delete). Do not remove the data (FR-012).
  - Past records keep showing the original league information (FR-012).
- **Related:** US-3.3, FR-005, FR-011, FR-012

### SCR-3.7: Confirm save message

- **Who can open it:** Owner only (shown after the owner clicks Save or Create copy)
- **Content:** A short question such as "Do you want to save this change?"
- **Buttons and links:** Confirm, Cancel
- **Rules:**
  - Nothing is saved until the owner clicks Confirm (FR-018).
  - Cancel returns the owner to the form with the information still filled in.
- **Related:** FR-018

### SCR-3.8: Public leagues page

- **Who can open it:** Everyone (no login needed)
- **Content:** Active leagues grouped by sport. Each league shows its name and sport.
- **Buttons and links:** Open a league
- **Rules:**
  - Show only leagues with the state Active (FR-013).
  - Do not show any edit buttons.
  - Do not ask for login.
- **Related:** US-3.9, FR-013

### SCR-3.9: Public league page

- **Who can open it:** Everyone (no login needed)
- **Content:** The league name, sport, description, the seasons of the league and the teams of the league
- **Buttons and links:** Open a team or season (if those pages exist), Back to leagues
- **Rules:**
  - Do not show any edit buttons.
  - If the league is Inactive or Deleted, do not show the page.
- **Related:** US-3.9

### Rules for all screens

- Every screen MUST work on an office computer and on a phone (FR-017).
- Only the owner can change information. Other roles MUST be rejected (FR-016).
- Error messages MUST be short and clear.

-----

## Key Entities

- **League** — A group of teams that play each other in one sport, for example Fall League.

-----

## Initial Data Model

### League

- league_id: String — Required, unique
- sport_id: String — Required
- name: String — Required
- games_per_team: Integer — Required
- min_players: Integer — Required
- max_players: Integer — Required
- description: String — Optional
- record_state: String — Required (Active, Inactive, Deleted). Deleted is a soft delete, see shared/GLOSSARY.md

-----

## Gherkin AC

### US-3.1 — Add league

#### Scenario: League is saved

- **Given** a league does not already exist
- **When** the owner enters the required league information and saves
- **Then** the system saves the league

#### Scenario: League is not saved due to missing information

- **Given** a league is being added
- **When** the sport or another required value is missing
- **Then** the system does not save the league

#### Scenario: Duplicate league name is rejected

- **Given** "Fall League" exists in "Flag Football"
- **When** the owner adds another "Fall League" in "Flag Football"
- **Then** the system rejects the duplicate league

#### Scenario: Wrong role cannot change information

- **Given** a manager is signed in
- **When** the manager tries to change information in this feature
- **Then** the system rejects the change

#### Scenario: Confirm before saving

- **Given** the user changes information
- **When** the user clicks save
- **Then** the system asks the user to confirm

### US-3.2 — Edit league

#### Scenario: League is edited successfully

- **Given** a league exists
- **When** the owner changes the league information and saves
- **Then** the system saves the updated league

#### Scenario: Player limits are checked

- **Given** a league exists
- **When** the owner sets the minimum players higher than the maximum
- **Then** the system does not save the update

### US-3.3 — Delete league

#### Scenario: League is deleted successfully

- **Given** a league exists and has no teams or seasons
- **When** the owner deletes the league
- **Then** the system removes the league from active records

#### Scenario: League with teams cannot be deleted

- **Given** a league has teams
- **When** the owner tries to delete it
- **Then** the system rejects the delete operation
- **And** the league and the other records stay unchanged

#### Scenario: Deleted league does not change past records

- **Given** a league was deleted and past records refer to it
- **When** someone views those past records
- **Then** the system still shows the original league information

#### Scenario: Delete unknown league fails

- **Given** the league does not exist
- **When** the owner tries to delete it
- **Then** the system rejects the delete operation

### US-3.4 — View league

#### Scenario: League information is displayed

- **Given** a league exists with teams and seasons
- **When** the owner views the league
- **Then** the system displays the league information, its teams and its seasons

### US-3.5 — Set league rules

#### Scenario: Rules are saved

- **Given** a league exists
- **When** the owner sets 10 games per team and 8 to 12 players
- **Then** the system saves the rules

#### Scenario: Games per team must be positive

- **Given** a league is being edited
- **When** the owner enters 0 games per team
- **Then** the system does not save the league

### US-3.6 — Copy league

#### Scenario: League is copied

- **Given** "Fall League" has 10 games per team and 8 to 12 players per team
- **When** the owner copies it as "Spring League"
- **Then** the system creates "Spring League" with the same settings and no teams

### US-3.7 — Make league inactive

#### Scenario: Inactive league is hidden

- **Given** a league is made inactive
- **When** the public opens the league list
- **Then** the league is not shown
- **And** its seasons, games and stats stay in the system

### US-3.8 — Filter leagues by sport

#### Scenario: Filter by sport

- **Given** leagues exist in several sports
- **When** the owner filters by "Softball"
- **Then** the system shows only the softball leagues

### US-3.9 — Public views leagues

#### Scenario: Public sees a league page

- **Given** an active league exists
- **When** a person who is not logged in opens the league
- **Then** the system shows the seasons and the teams of the league
