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
