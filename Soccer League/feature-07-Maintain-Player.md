# Feature: Maintain Player

**Feature ID:** 7  
**Branch pattern:** `feature/7-maintain-player`  
**Status:** Draft  
**Created:** 2026-10-20  
**Input:** Maintain the players of each team.  
**Depends on:** [Feature 6-Maintain Team](Feature-6-Maintain-Team.md)

------

## User Stories

### US-7.1: Add player

**As a** manager  
**I want to** add a player to my team  
**So that** the player can play in games.  
**Priority:** P1  
**Independent test:** Add a player and verify that the player is on the roster.  
**Acceptance Scenarios:** see ### US-7.1 under Gherkin AC

### US-7.2: Edit player

**As a** manager  
**I want to** edit a player of my team  
**So that** the player information stays accurate.  
**Priority:** P1  
**Independent test:** Edit a player and verify that the change is saved.  
**Acceptance Scenarios:** see ### US-7.2 under Gherkin AC

### US-7.3: Remove player

**As a** manager  
**I want to** remove a player from my team  
**So that** players who left are not used anymore.  
**Priority:** P1  
**Independent test:** Remove a player and verify that old stats stay.  
**Acceptance Scenarios:** see ### US-7.3 under Gherkin AC

### US-7.4: View roster

**As a** manager  
**I want to** view my roster with each player's totals  
**So that** I know who is doing well.  
**Priority:** P1  
**Independent test:** Open the roster and verify that totals are displayed.  
**Acceptance Scenarios:** see ### US-7.4 under Gherkin AC

### US-7.5: Move player to another team

**As an** owner  
**I want to** move a player to another team  
**So that** transfers are recorded without losing the old stats.  
**Priority:** P2  
**Independent test:** Move a player and verify that old stats stay with the old team.  
**Acceptance Scenarios:** see ### US-7.5 under Gherkin AC

### US-7.6: Search players

**As an** owner  
**I want to** search players by name across the league  
**So that** I can find anyone fast.  
**Priority:** P3  
**Independent test:** Search a player name and verify that the player is found.  
**Acceptance Scenarios:** see ### US-7.6 under Gherkin AC

### US-7.7: Public views players

**As a** person from the public  
**I want to** open a player page with stats  
**So that** family and friends can follow the player.  
**Priority:** P2  
**Independent test:** Open a public player page and verify that stats show and contact details do not.  
**Acceptance Scenarios:** see ### US-7.7 under Gherkin AC

-----

## Functional Requirements

- **FR-001:** The system MUST maintain players.
- **FR-002:** Each player MUST have a unique identifier.
- **FR-003:** The system MUST allow authorized users to add players.
- **FR-004:** The system MUST allow authorized users to edit players.
- **FR-005:** The system MUST allow authorized users to delete players.
- **FR-006:** The system MUST allow authorized users to view players.
- **FR-007:** Required player information MUST be provided before the player can be saved (name, team, jersey number).
- **FR-008:** A jersey number MUST be unique inside a team.
- **FR-009:** A team MUST NOT have more players than the league maximum.
- **FR-010:** The system MUST warn when a player with the same email already exists.
- **FR-011:** Removing a player MUST only make the player Inactive, so their old game stats stay in the records.
- **FR-012:** A player MUST NOT be active on two teams of the same league at the same time.
- **FR-013:** The system MUST let the owner move a player to another team. Old stats MUST stay with the old team.
- **FR-014:** The system MUST let the owner search players by name across the league.
- **FR-015:** A manager MUST be able to add, edit and remove players only on their own team. The owner MUST be able to do it on any team.
- **FR-016:** The public pages MUST show only the player's name, team and stats. Email and phone MUST stay private.
- **FR-017:** The system MUST work on an office computer and on a phone.

-----

## Screen Requirements

### SCR-7.1: Roster page

- **Who can open it:** Manager (own team only) and owner (any team)
- **Content:** A table of the players of a team with these columns: Jersey number, Name, Position, Record state, Totals (stats of the player)
- **Fields:** Team (owner only, choose a team)
- **Buttons and links:** Add player, View, Edit, Remove, Move to another team (owner only)
- **Rules:**
  - A manager sees only the roster of their own team (FR-015).
  - The owner can open the roster of any team (FR-015).
  - Show the totals of each player (US-7.4).
  - Players with the state Inactive are marked as Inactive.
  - Other roles cannot open this page.
- **Related:** US-7.1, US-7.2, US-7.3, US-7.4, FR-006, FR-015

### SCR-7.2: Add player page

- **Who can open it:** Manager (own team only) and owner (any team)
- **Fields:** Team (required. A manager sees only their own team. The owner can choose a team), Name (required), Jersey number (required), Position (optional), Email (optional), Phone (optional)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - If a required field is empty, do not save and show which field is missing (FR-007).
  - Reject a jersey number that is already used in the same team (FR-008).
  - Reject the player if the team already has the league maximum number of players (FR-009).
  - If a player with the same email already exists, show a warning (FR-010).
  - If the player is already active on another team of the same league, reject the player and tell the manager to ask the owner to move the player (FR-012).
  - After saving, the player is on the roster.
- **Related:** US-7.1, FR-003, FR-007, FR-008, FR-009, FR-010, FR-012, FR-015

### SCR-7.3: Edit player page

- **Who can open it:** Manager (own team only) and owner (any team)
- **Fields:** Name (required), Jersey number (required), Position (optional), Email (optional), Phone (optional)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - Show the current information of the player when the page opens.
  - If a required field is removed, do not save the change (FR-007).
  - Reject a jersey number that is already used in the same team (FR-008).
  - If a player with the same email already exists, show a warning (FR-010).
  - A manager who opens a player of another team is rejected (FR-015).
- **Related:** US-7.2, FR-004, FR-007, FR-008, FR-010, FR-015

### SCR-7.4: Remove player confirm message

- **Who can open it:** Manager (own team only) and owner (any team). Shown after the user clicks Remove.
- **Content:** The player name and a question such as "Do you want to remove this player?"
- **Buttons and links:** Confirm remove, Cancel
- **Rules:**
  - Removing only makes the player Inactive. The player is not deleted (FR-011).
  - The old game stats of the player stay in the records (FR-011).
  - If the player does not exist, reject the operation.
- **Related:** US-7.3, FR-005, FR-011, FR-015

### SCR-7.5: Move player page

- **Who can open it:** Owner only
- **Fields:** New team (required), Jersey number (required, starts with the current number)
- **Buttons and links:** Move player, Cancel
- **Rules:**
  - Show the current team of the player when the page opens.
  - After the move, the player is on the roster of the new team (FR-013).
  - Old stats stay with the old team (FR-013).
  - The jersey number must be unique in the new team (FR-008).
  - Reject the move if the new team already has the league maximum number of players (FR-009).
  - The player must not be active on two teams of the same league (FR-012).
- **Related:** US-7.5, FR-008, FR-009, FR-012, FR-013

### SCR-7.6: Search players page

- **Who can open it:** Owner only
- **Fields:** Search box (search by player name)
- **Content:** A list of matching players with these columns: Name, Jersey number, Team, Record state
- **Buttons and links:** View
- **Rules:**
  - Search finds players by part of the name across the league (FR-014).
  - If nothing is found, show "No player found".
- **Related:** US-7.6, FR-014

### SCR-7.7: View player page

- **Who can open it:** Manager (own team only) and owner (any team)
- **Content:** Player information (Name, Team, Jersey number, Position, Email, Phone, Record state), totals, and the stats of each game
- **Buttons and links:** Edit, Remove, Back to roster
- **Rules:**
  - Show the information as read only.
  - A manager sees only players of their own team (FR-015).
- **Related:** US-7.4, FR-006, FR-015

### SCR-7.8: Public player page

- **Who can open it:** Everyone (no login needed)
- **Content:** The player name, team, and the stats of each game
- **Buttons and links:** Back to team
- **Rules:**
  - Show only the name, team and stats (FR-016).
  - Do not show the email or the phone (FR-016).
  - Do not show any edit buttons.
  - Do not ask for login.
- **Related:** US-7.7, FR-016

### Rules for all screens

- Every screen MUST work on an office computer and on a phone (FR-017).
- A manager can change information only on their own team. The owner can change information on any team. Other roles MUST be rejected (FR-015).
- Error messages MUST be short and clear.

-----

## Key Entities

- **Player** — A person who plays for a team.

-----

## Initial Data Model

### Player

- player_id: String — Required, unique
- team_id: String — Required
- name: String — Required
- jersey_number: Integer — Required, unique in the team
- position: String — Optional
- email: String — Optional
- phone: String — Optional
- record_state: String — Required (Active, Inactive, Deleted). Deleted is a soft delete, see shared/GLOSSARY.md

-----

## Gherkin AC

### US-7.1 — Add player

#### Scenario: Player is saved

- **Given** a player does not already exist
- **When** the manager enters the required player information and saves
- **Then** the system saves the player on the roster

#### Scenario: Player is not saved due to missing information

- **Given** a player is being added
- **When** required player information is missing
- **Then** the system does not save the player

#### Scenario: Jersey number is already used

- **Given** "Eagles" already has player number 10
- **When** the manager adds another player with number 10
- **Then** the system rejects the player

#### Scenario: Roster is full

- **Given** the league maximum is 12 and "Eagles" has 12 players
- **When** the manager adds one more player
- **Then** the system rejects the player

#### Scenario: Same email warning

- **Given** a player with the email john@example.com exists
- **When** the manager adds a player with the same email
- **Then** the system warns that a player with this email already exists

#### Scenario: Player is already on another team

- **Given** John is active on "Eagles" in "Fall League"
- **When** the manager of "Hawks" adds John to "Hawks" in "Fall League"
- **Then** the system rejects the player and tells the manager to ask the owner to move the player

#### Scenario: Wrong role cannot change information

- **Given** a ref is signed in
- **When** the ref tries to change information in this feature
- **Then** the system rejects the change

### US-7.2 — Edit player

#### Scenario: Player is edited successfully

- **Given** a player exists on the manager's team
- **When** the manager changes the player information and saves
- **Then** the system saves the updated player

#### Scenario: Manager cannot edit another team's player

- **Given** a manager of "Eagles" is signed in
- **When** the manager tries to edit a player of "Hawks"
- **Then** the system rejects the change

### US-7.3 — Remove player

#### Scenario: Player is removed

- **Given** a player exists
- **When** the manager removes the player
- **Then** the system makes the player Inactive

#### Scenario: Stats stay after removal

- **Given** John played 3 games
- **When** the manager removes John
- **Then** John's stats from those 3 games are still in the records

#### Scenario: Remove unknown player fails

- **Given** the player does not exist
- **When** the manager tries to remove the player
- **Then** the system rejects the operation

### US-7.4 — View roster

#### Scenario: Roster is displayed

- **Given** a team has players
- **When** the manager opens the roster
- **Then** the system displays the players with their totals

### US-7.5 — Move player to another team

#### Scenario: Player is moved

- **Given** John plays for "Eagles"
- **When** the owner moves John to "Hawks"
- **Then** John is on the "Hawks" roster

#### Scenario: Old stats stay with the old team

- **Given** John has 3 games with "Eagles" and is moved to "Hawks"
- **When** someone views the old games
- **Then** the 3 games still show under "Eagles"

### US-7.6 — Search players

#### Scenario: Search finds a player

- **Given** players exist
- **When** the owner searches for part of a name
- **Then** the system shows the matching players with their teams

### US-7.7 — Public views players

#### Scenario: Public sees player stats

- **Given** a player has stats
- **When** a person who is not logged in opens the player page
- **Then** the system shows the name, team and stats of each game

#### Scenario: Contact details stay private

- **Given** a player has an email and a phone
- **When** a person who is not logged in opens the player page
- **Then** the system does not show the email or the phone
