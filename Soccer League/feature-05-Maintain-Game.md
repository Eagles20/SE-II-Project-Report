# Feature: Maintain Game

**Feature ID:** 5  
**Branch pattern:** `feature/5-maintain-game`  
**Status:** Draft  
**Created:** 2026-10-20  
**Input:** Maintain games (date, time, teams, location, status) for a season.  
**Depends on:**    [feature 4 — Maintain- Season](feature-4-Maintain-Season.md), [feature 6 - Maintain-Team](feature-6-Maintain-Team.md), [feature 8 -Maintain-Location](feature-8-Maintain-Location.md)

------

## User Stories

### US-5.1: Add game

**As an** owner  
**I want to** add a game by hand  
**So that** I can add a game the generator did not make.  
**Priority:** P1  
**Independent test:** Add a game and verify that it is saved.  
**Acceptance Scenarios:** see ### US-5.1 under Gherkin AC

### US-5.2: Edit game date and time

**As an** owner  
**I want to** change the date or time of a game  
**So that** I can reschedule it.  
**Priority:** P1  
**Independent test:** Change a game time and verify that the change is saved.  
**Acceptance Scenarios:** see ### US-5.2 under Gherkin AC

### US-5.3: Change location of one game

**As an** owner  
**I want to** change the location of only one game  
**So that** a field problem does not change the team's home location.  
**Priority:** P1  
**Independent test:** Change one game location and verify that the team home location is the same.  
**Acceptance Scenarios:** see ### US-5.3 under Gherkin AC

### US-5.4: Cancel game

**As an** owner  
**I want to** cancel a game and give a reason  
**So that** everyone can see why it was cancelled.  
**Priority:** P1  
**Independent test:** Cancel a game and verify that the reason is shown.  
**Acceptance Scenarios:** see ### US-5.4 under Gherkin AC

### US-5.5: Postpone game

**As an** owner  
**I want to** postpone a game and set a new date later  
**So that** the game is not lost.  
**Priority:** P2  
**Independent test:** Postpone a game and verify that its status changes.  
**Acceptance Scenarios:** see ### US-5.5 under Gherkin AC

### US-5.6: Delete game

**As an** owner  
**I want to** delete a game  
**So that** a game made by mistake can be removed.  
**Priority:** P1  
**Independent test:** Delete a game and verify that it is no longer active.  
**Acceptance Scenarios:** see ### US-5.6 under Gherkin AC

### US-5.7: View and filter games

**As an** owner  
**I want to** view games and filter them by date, team, location, ref or status  
**So that** I can find a game fast.  
**Priority:** P1  
**Independent test:** Filter games by team and verify that only its games are shown.  
**Acceptance Scenarios:** see ### US-5.7 under Gherkin AC

### US-5.8: View my games

**As a** manager  
**I want to** view the games of my team  
**So that** I can prepare my players.  
**Priority:** P2  
**Independent test:** Log in as a manager and verify that only the team games are shown.  
**Acceptance Scenarios:** see ### US-5.8 under Gherkin AC

### US-5.9: Public views games

**As a** person from the public  
**I want to** see upcoming games and cancelled games with the reason  
**So that** I can go and watch and I do not travel for nothing.  
**Priority:** P2  
**Independent test:** Open the public schedule and verify that games and reasons are shown.  
**Acceptance Scenarios:** see ### US-5.9 under Gherkin AC

-----

## Functional Requirements

- **FR-001:** The system MUST maintain games.
- **FR-002:** Each game MUST have a unique identifier.
- **FR-003:** The system MUST allow authorized users to add games.
- **FR-004:** The system MUST allow authorized users to edit games.
- **FR-005:** The system MUST allow authorized users to delete games.
- **FR-006:** The system MUST allow authorized users to view games.
- **FR-007:** Required game information MUST be provided before the game can be saved (season, home team, away team, date, time, location).
- **FR-008:** The home team and the away team MUST be different and MUST be in the same league.
- **FR-009:** A game date MUST be inside the season dates, and a game MUST NOT be added to a Completed season.
- **FR-010:** A game MUST have a status: Scheduled, Completed, Postponed or Cancelled.
- **FR-011:** Cancelling a game MUST need a reason.
- **FR-012:** The system MUST NOT cancel a game that has a result.
- **FR-013:** The system MUST warn the owner when a team or a location is already used at the same date and time.
- **FR-014:** The system MUST let the owner change the location of one game without changing the team's home location.
- **FR-015:** The system MUST NOT delete a game that has a result.
- **FR-016:** Deleting a game MUST be a soft delete (record state Deleted), so other features keep the original game information.
- **FR-017:** The system MUST let the owner filter games by date, team, location, ref and status.
- **FR-018:** The system MUST keep a history of changes to a game (date, time, location, status, cancel reason) with who and when.
- **FR-019:** A manager MUST be able to view the games of their own team, and a ref MUST be able to view their own games.
- **FR-020:** The system MUST let the owner use this feature (main user: owner), and MUST NOT let other roles change its information.
- **FR-021:** The system MUST work on an office computer and on a phone.

-----

## Screen Requirements

### SCR-5.1: Game list page

- **Who can open it:** Owner only
- **Content:** A table of games with these columns: Date, Time, Season, Home team, Away team, Location, Status
- **Fields:** Filters: Date, Team, Location, Ref, Status
- **Buttons and links:** Add game, View, Edit date and time, Change location, Postpone, Cancel, Delete
- **Rules:**
  - The owner can filter games by date, team, location, ref and status (FR-017).
  - Games with the state Deleted are not shown in the list.
  - Other roles cannot open this page. Managers and refs use SCR-5.9 (FR-020).
- **Related:** US-5.7, FR-006, FR-017, FR-020

### SCR-5.2: Add game page

- **Who can open it:** Owner only
- **Fields:** Season (required), Home team (required), Away team (required), Date (required), Time (required), Location (required)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - If a required field is empty, do not save and show which field is missing (FR-007).
  - The home team and the away team must be different and in the same league (FR-008).
  - The date must be inside the season dates. Do not add a game to a Completed season (FR-009).
  - If a team or the location is already used at the same date and time, show a warning (FR-013).
  - A new game starts with the status Scheduled.
- **Related:** US-5.1, FR-003, FR-007, FR-008, FR-009, FR-013

### SCR-5.3: Edit game date and time page

- **Who can open it:** Owner only
- **Fields:** Date (required), Time (required)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - Show the current date and time when the page opens.
  - If a team or the location is already used at the new date and time, show a warning (FR-013).
  - Save the change in the game history: who changed it, when, and the old and new value (FR-018).
- **Related:** US-5.2, FR-004, FR-013, FR-018

### SCR-5.4: Change game location page

- **Who can open it:** Owner only
- **Fields:** Location (required)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - Show the current location when the page opens.
  - The change is only for this game. The home location of the team stays the same (FR-014).
  - If the new location is already used at the same date and time, show a warning (FR-013).
  - Save the change in the game history (FR-018).
- **Related:** US-5.3, FR-013, FR-014, FR-018

### SCR-5.5: Cancel game page

- **Who can open it:** Owner only
- **Fields:** Cancel reason (required)
- **Buttons and links:** Cancel the game, Back
- **Rules:**
  - If the reason is empty, do not cancel the game (FR-011).
  - If the game has a result, reject the cancel (FR-012).
  - After cancelling, the game shows the status Cancelled and the reason.
  - Save the change in the game history (FR-018).
- **Related:** US-5.4, FR-011, FR-012, FR-018

### SCR-5.6: Postpone game page

- **Who can open it:** Owner only
- **Fields:** New date (optional), New time (optional)
- **Buttons and links:** Postpone, Back
- **Rules:**
  - The owner can postpone a game now and set the new date and time later.
  - After postponing, the game shows the status Postponed.
  - When the owner sets a new date and time for a Postponed game, the game shows the status Scheduled with the new date and time.
  - The new date must be inside the season dates (FR-009).
  - Save the change in the game history (FR-018).
- **Related:** US-5.5, FR-009, FR-010, FR-018

### SCR-5.7: Delete confirm message

- **Who can open it:** Owner only (shown after the owner clicks Delete)
- **Content:** The game (teams, date and time) and a question such as "Do you want to delete this game?"
- **Buttons and links:** Confirm delete, Cancel
- **Rules:**
  - If the game has a result, reject the delete and show a message. The game and its result stay unchanged (FR-015).
  - If the game has no result, change the record state to Deleted (soft delete). Do not remove the data (FR-016).
- **Related:** US-5.6, FR-005, FR-015, FR-016

### SCR-5.8: View game page

- **Who can open it:** Owner only
- **Content:** Season, Home team, Away team, Date, Time, Location, Status, Cancel reason (when cancelled), and the change history (what changed, old value, new value, who, when)
- **Buttons and links:** Edit date and time, Change location, Postpone, Cancel, Delete, Back to list
- **Rules:**
  - Show the information as read only.
  - Show the change history of the game (FR-018).
- **Related:** US-5.7, FR-006, FR-018

### SCR-5.9: My games page (manager and ref)

- **Who can open it:** Manager and ref (login needed)
- **Content:** A table of games with these columns: Date, Time, Home team, Away team, Location, Status
- **Rules:**
  - A manager sees only the games of their own team (FR-019).
  - A ref sees only the games assigned to the ref (FR-019).
  - The page is read only. Do not show any edit buttons (FR-020).
- **Related:** US-5.8, FR-019, FR-020

### SCR-5.10: Public schedule page

- **Who can open it:** Everyone (no login needed)
- **Content:** A list of games. Each game shows date, time, teams, location and status. A cancelled game shows the cancel reason.
- **Buttons and links:** Open a game
- **Rules:**
  - Show upcoming games, and show cancelled games with the reason (US-5.9).
  - Do not show any edit buttons.
  - Do not ask for login.
- **Related:** US-5.9

### SCR-5.11: Public game page

- **Who can open it:** Everyone (no login needed)
- **Content:** Teams, date, time, location, status, and the cancel reason when the game is cancelled
- **Buttons and links:** Back to schedule
- **Rules:**
  - Do not show any edit buttons.
  - Do not show the change history to the public.
  - Do not show a game with the state Deleted.
- **Related:** US-5.9

### Rules for all screens

- Every screen MUST work on an office computer and on a phone (FR-021).
- Only the owner can change information. Other roles MUST be rejected (FR-020).
- Error messages MUST be short and clear.

-----

## Key Entities

- **Game** — One match between a home team and an away team at a date, time and location.
- **Game change history** — The record of who changed a game and when.

-----

## Initial Data Model

### Game

- game_id: String — Required, unique
- season_id: String — Required
- home_team_id: String — Required
- away_team_id: String — Required, different from home team
- game_date: Date — Required
- game_time: Time — Required
- location_id: String — Required
- status: String — Required (Scheduled, Completed, Postponed, Cancelled)
- cancel_reason: String — Required when cancelled
- record_state: String — Required (Active, Inactive, Deleted). Deleted is a soft delete, see shared/GLOSSARY.md

### Game change history

- change_id: String — Required, unique
- game_id: String — Required
- field_changed: String — Required
- old_value: String — Required
- new_value: String — Required
- changed_by: String — Required
- changed_at: DateTime — Required

-----

## Gherkin AC

### US-5.1 — Add game

#### Scenario: Game is saved

- **Given** a season and two teams exist
- **When** the owner enters the required game information and saves
- **Then** the system saves the game with the status Scheduled

#### Scenario: Game is not saved due to missing information

- **Given** a game is being added
- **When** required game information is missing
- **Then** the system does not save the game

#### Scenario: Same team on both sides is rejected

- **Given** a game is being added
- **When** the owner chooses "Eagles" as home and away team
- **Then** the system does not save the game

#### Scenario: Game outside season dates is rejected

- **Given** "Fall 2026" ends on Dec 10
- **When** the owner adds a game on Dec 20
- **Then** the system does not save the game

#### Scenario: Game in a Completed season is rejected

- **Given** a season is Completed
- **When** the owner adds a game to it
- **Then** the system does not save the game

#### Scenario: Wrong role cannot change information

- **Given** a manager is signed in
- **When** the manager tries to change information in this feature
- **Then** the system rejects the change

### US-5.2 — Edit game date and time

#### Scenario: Game is edited successfully

- **Given** a game exists
- **When** the owner changes the date or time and saves
- **Then** the system saves the updated game

#### Scenario: Team is already busy

- **Given** "Eagles" plays at 6 PM on Oct 25
- **When** the owner moves another "Eagles" game to 6 PM that day
- **Then** the system warns that the team already has a game at that time

#### Scenario: Game change is recorded

- **Given** a game is at 6 PM
- **When** the owner moves it to 7 PM
- **Then** the system records who changed it, when, and the old and new time

### US-5.3 — Change location of one game

#### Scenario: Game location changes

- **Given** a game is at "Field A"
- **When** the owner changes the location to "Field B"
- **Then** the game shows "Field B"
- **And** the team home location stays the same

#### Scenario: Location is already used

- **Given** "Field B" has a game at 6 PM
- **When** the owner puts another game at "Field B" at 6 PM
- **Then** the system warns that the location is already used

### US-5.4 — Cancel game

#### Scenario: Game is cancelled with a reason

- **Given** a game is scheduled
- **When** the owner cancels it with the reason "Rain"
- **Then** the game shows Cancelled and the reason "Rain"

#### Scenario: Cancel without a reason fails

- **Given** a game is scheduled
- **When** the owner cancels it without a reason
- **Then** the system does not cancel the game

#### Scenario: Game with a result cannot be cancelled

- **Given** a game has a result
- **When** the owner tries to cancel it
- **Then** the system rejects the change

### US-5.5 — Postpone game

#### Scenario: Game is postponed

- **Given** a game is scheduled
- **When** the owner postpones it
- **Then** the game shows Postponed

#### Scenario: Postponed game gets a new date

- **Given** a game is Postponed
- **When** the owner sets a new date and time
- **Then** the game shows Scheduled with the new date and time

### US-5.6 — Delete game

#### Scenario: Game is deleted successfully

- **Given** a game exists and has no result
- **When** the owner deletes the game
- **Then** the system removes the game from active records

#### Scenario: Game with a result cannot be deleted

- **Given** a game has a result
- **When** the owner tries to delete it
- **Then** the system rejects the delete operation
- **And** the game and its result stay unchanged

#### Scenario: Delete unknown game fails

- **Given** the game does not exist
- **When** the owner tries to delete it
- **Then** the system rejects the delete operation

### US-5.7 — View and filter games

#### Scenario: Games are displayed

- **Given** games exist
- **When** the owner opens the game list
- **Then** the system displays the games

#### Scenario: Filter by team

- **Given** games exist for several teams
- **When** the owner filters by "Eagles"
- **Then** the system shows only games with "Eagles"

### US-5.8 — View my games

#### Scenario: Manager sees own team games

- **Given** a manager is signed in
- **When** the manager opens the game list
- **Then** the system shows only the games of the manager's team

#### Scenario: Ref sees own games

- **Given** a ref is signed in
- **When** the ref opens the game list
- **Then** the system shows only the games assigned to the ref

### US-5.9 — Public views games

#### Scenario: Public sees upcoming games

- **Given** games are scheduled
- **When** a person who is not logged in opens the schedule
- **Then** the system shows date, time and location of each game

#### Scenario: Public sees cancelled game reason

- **Given** a game was cancelled with the reason "Rain"
- **When** a person opens the game
- **Then** the system shows Cancelled and the reason
