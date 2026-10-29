# Feature: Game Results and Stats

**Feature ID:** 11  
**Branch pattern:** `feature/11-game-results-and-stats`  
**Status:** Draft  
**Created:** 2026-10-21  
**Input:** Let managers enter game results and player stats, and build standings and totals.  
**Depends on:** [Feature 5-Maintain Game](Feature-5-Maintain-Game.md), [Feature 7-Maintain-Player](Feature-7-Maintain-Player.md)

------

## User Stories

### US-11.1: Enter result

**As a** manager  
**I want to** enter the score of each team after my game  
**So that** the result is saved and shown.  
**Priority:** P1  
**Independent test:** Enter a score and verify that it is saved.  
**Acceptance Scenarios:** see ### US-11.1 under Gherkin AC

### US-11.2: Enter player stats

**As a** manager  
**I want to** enter stats for each player in the game  
**So that** every player has their own record.  
**Priority:** P1  
**Independent test:** Enter stats for a player and verify that they are saved.  
**Acceptance Scenarios:** see ### US-11.2 under Gherkin AC

### US-11.3: Enter forfeit

**As a** manager  
**I want to** enter a forfeit when a team did not show up  
**So that** the result is correct without playing.  
**Priority:** P2  
**Independent test:** Enter a forfeit and verify the winner.  
**Acceptance Scenarios:** see ### US-11.3 under Gherkin AC

### US-11.4: Change my result within 48 hours

**As a** manager  
**I want to** change a result within 48 hours  
**So that** I can fix a typing mistake.  
**Priority:** P1  
**Independent test:** Change a result right after entering it and verify that it is saved.  
**Acceptance Scenarios:** see ### US-11.4 under Gherkin AC

### US-11.5: Correct a result as owner

**As an** owner  
**I want to** correct any result or stat at any time  
**So that** the records are right.  
**Priority:** P1  
**Independent test:** Correct an old result and verify that it is saved.  
**Acceptance Scenarios:** see ### US-11.5 under Gherkin AC

### US-11.6: See change history

**As an** owner  
**I want to** see who changed a result or stat and when  
**So that** changes are clear.  
**Priority:** P2  
**Independent test:** Change a score and verify that the history shows it.  
**Acceptance Scenarios:** see ### US-11.6 under Gherkin AC

### US-11.7: Set stat types for a sport

**As an** owner  
**I want to** set the stat types for each sport  
**So that** the right stats are collected.  
**Priority:** P1  
**Independent test:** Set stat types for basketball and verify that they appear when entering stats.  
**Acceptance Scenarios:** see ### US-11.7 under Gherkin AC

### US-11.8: Mark player did not play

**As a** manager  
**I want to** mark a player as "did not play"  
**So that** stats are not wrong.  
**Priority:** P2  
**Independent test:** Mark a player and verify that the player gets no stats.  
**Acceptance Scenarios:** see ### US-11.8 under Gherkin AC

### US-11.9: See games without a result

**As a** manager  
**I want to** see my finished games that have no result  
**So that** I do not forget to enter them.  
**Priority:** P2  
**Independent test:** Open the list and verify that it shows the games.  
**Acceptance Scenarios:** see ### US-11.9 under Gherkin AC

### US-11.10: Standings and leaders

**As a** person from the public  
**I want to** see the team standings, the box score of a game, and the leaders  
**So that** I know who is leading and how each player did.  
**Priority:** P1  
**Independent test:** Enter results and verify that standings and leaders update.  
**Acceptance Scenarios:** see ### US-11.10 under Gherkin AC

### US-11.11: Confirm or dispute a result

**As a** manager  
**I want to** confirm or dispute the result entered by the other team's manager  
**So that** both teams agree on the score.  
**Priority:** P1  
**Independent test:** Enter a result as one manager and verify that the other manager can confirm or dispute it.  
**Acceptance Scenarios:** see ### US-11.11 under Gherkin AC

-----

## Functional Requirements

- **FR-001:** The system MUST let a manager enter the result (score for each team) only for games of their own team.
- **FR-002:** The system MUST let a manager enter stats for each player of the two teams in the game, and MUST NOT accept stats for other players.
- **FR-003:** Each game MUST have one result, and each player MUST have one stat record for each game.
- **FR-004:** The stat types MUST be set by sport (for example points for basketball, touchdowns for flag football, hits and runs for softball).
- **FR-005:** The system MUST let a manager enter a forfeit. The result MUST show the forfeit and the winner.
- **FR-006:** The system MUST let a manager mark a player as "did not play" for a game.
- **FR-007:** The system MUST let a manager change a result only within 48 hours after entering it. After that only the owner MUST be able to change it.
- **FR-008:** The system MUST NOT keep two results for the same game. After one manager enters a result, the manager of the other team MUST be able to confirm or dispute it within 48 hours.
- **FR-009:** A disputed result MUST go to the owner. The owner's decision MUST be final and MUST be saved in the change history.
- **FR-010:** The system MUST let the owner correct any result or stat at any time.
- **FR-011:** The system MUST keep a change history for results and stats (who, when, old value, new value).
- **FR-012:** The system MUST show a manager the finished games of their team that have no result.
- **FR-013:** The system MUST NOT accept a result or stat change in a Completed season, except by the owner after reopening it.
- **FR-014:** The system MUST keep results and stats forever, so records are never lost.
- **FR-015:** The system MUST update each player's totals and the team standings (wins, losses, ties) from the results.
- **FR-016:** The system MUST build leader lists (for example top scorers) from the stats.
- **FR-017:** The system MUST let the owner and the managers use this feature (main user: manager), and MUST NOT let a ref or the public change results or stats.
- **FR-018:** The system MUST work on a phone, so a manager can enter a score at the field, and on an office computer.

-----

## Screen Requirements

### SCR-11.1: Games without a result page

- **Who can open it:** Manager (own team only)
- **Content:** A table of the finished games of the manager's team that have no result. Each game shows date, time, teams and location.
- **Buttons and links:** Enter result
- **Rules:**
  - Show only finished games of the manager's own team that have no result (FR-012).
  - If there are no such games, show "No games without a result".
  - A manager sees only games of their own team (FR-001).
- **Related:** US-11.9, FR-001, FR-012

### SCR-11.2: Enter or change result page

- **Who can open it:** Manager (games of their own team only) and owner (any game)
- **Fields:** Home score (required), Away score (required), Forfeit (checkbox, and choose the team that did not show up)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - If a score is missing, do not save the result (US-11.1).
  - A manager can enter a result only for a game of their own team (FR-001).
  - A game has only one result. If the game already has a result, do not create a second one and offer to dispute the existing one (FR-003, FR-008).
  - For a forfeit, the result shows the forfeit and the other team as the winner (FR-005).
  - A manager can change a result only within 48 hours after entering it. After that, show a message that only the owner can change it (FR-007).
  - The owner can change any result at any time (FR-010).
  - Do not accept a change in a Completed season. The owner must reopen the season first (FR-013).
  - After saving, the game shows Completed.
  - Save every change in the change history (FR-011).
  - After saving a result, show a link to enter the player stats.
- **Related:** US-11.1, US-11.3, US-11.4, US-11.5, FR-001, FR-003, FR-005, FR-007, FR-008, FR-010, FR-011, FR-013

### SCR-11.3: Enter or change player stats page

- **Who can open it:** Manager (games of their own team only) and owner (any game)
- **Content:** The players of both teams in the game. Each player has one row.
- **Fields:** For each player: Did not play (checkbox), and one number for each stat type of the sport (for example points and rebounds for basketball)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - Show only the players of the two teams in the game. Do not accept stats for other players (FR-002).
  - Each player has one stat record for the game (FR-003).
  - Ask for the stat types set for the sport of the game (FR-004).
  - When a player is marked "did not play," the player gets no stats for that game (FR-006).
  - A manager can change stats only within the same time rules as the result. After that only the owner can change them (FR-007, FR-010).
  - Do not accept a change in a Completed season. The owner must reopen the season first (FR-013).
  - After saving, the totals of the players are updated (FR-015).
  - Save every change in the change history (FR-011).
- **Related:** US-11.2, US-11.8, FR-002, FR-003, FR-004, FR-006, FR-011, FR-013, FR-015

### SCR-11.4: Confirm or dispute result page

- **Who can open it:** Manager of the other team (the team that did not enter the result)
- **Content:** The game, the entered score and who entered it
- **Buttons and links:** Confirm, Dispute
- **Rules:**
  - The manager has 48 hours to confirm or dispute the result (FR-008).
  - After Confirm, the result shows Confirmed.
  - After Dispute, the result shows Disputed and goes to the owner (FR-009).
  - A manager cannot confirm or dispute a game of another team (FR-001).
- **Related:** US-11.11, FR-008, FR-009

### SCR-11.5: Disputed results page

- **Who can open it:** Owner only
- **Content:** A table of the disputed results. Each row shows game, teams, entered score and the managers.
- **Buttons and links:** Decide
- **Rules:**
  - Show the results with the status Disputed (FR-009).
  - If there are none, show "No disputed results".
- **Related:** US-11.11, FR-009

### SCR-11.6: Decide disputed result page

- **Who can open it:** Owner only
- **Fields:** Home score (required), Away score (required)
- **Buttons and links:** Save decision, Cancel
- **Rules:**
  - The owner's decision is final (FR-009).
  - After saving, the result shows Confirmed.
  - Save the decision in the change history, with who decided (FR-009, FR-011).
- **Related:** US-11.11, FR-009, FR-011

### SCR-11.7: Change history page

- **Who can open it:** Owner only
- **Content:** A table of the changes to results and stats. Each row shows the record (result or stat), who changed it, when, the old value and the new value.
- **Rules:**
  - Show the history for results and stats (FR-011).
  - For example, a score changed from 21-14 to 24-14 shows who changed it, when, and the old and new score.
- **Related:** US-11.6, FR-011

### SCR-11.8: Stat types page

- **Who can open it:** Owner only
- **Fields:** Sport (required, choose a sport), Stat type name (required, for example points)
- **Content:** The list of stat types of the chosen sport
- **Buttons and links:** Add stat type, Back
- **Rules:**
  - Stat types are set by sport (FR-004).
  - The stat types of a sport are the ones that managers must fill when they enter stats.
- **Related:** US-11.7, FR-004

### SCR-11.9: Public standings page

- **Who can open it:** Everyone (no login needed)
- **Content:** A table of the teams of a league with these columns: Team, Wins, Losses, Ties
- **Buttons and links:** Open a team
- **Rules:**
  - Update the standings from the results (FR-015).
  - Do not show any edit buttons.
  - Do not ask for login.
- **Related:** US-11.10, FR-015

### SCR-11.10: Public box score page

- **Who can open it:** Everyone (no login needed)
- **Content:** The game, the score (with Forfeit when it is a forfeit), and the stats of each player
- **Buttons and links:** Back to schedule
- **Rules:**
  - Show the score and the stats of each player (US-11.10).
  - Do not show any edit buttons.
- **Related:** US-11.10, FR-005

### SCR-11.11: Public leaders page

- **Who can open it:** Everyone (no login needed)
- **Content:** A list of the leaders for each stat type of a sport, for example the top scorers in order
- **Rules:**
  - Build the lists from the stats (FR-016).
  - Do not show any edit buttons.
  - Do not ask for login.
- **Related:** US-11.10, FR-016

### Rules for all screens

- Every screen MUST work on a phone, so a manager can enter a score at the field, and on an office computer (FR-018).
- Only the owner and the managers can change results or stats. A ref and the public MUST be rejected (FR-017).
- Error messages MUST be short and clear.

-----

## Key Entities

- **Result** — The final score of a game.
- **Player stat** — The numbers of one player in one game.
- **Stat type** — A kind of number tracked for a sport (for example points).
- **Change history** — The record of who changed a result or stat and when.

-----

## Initial Data Model

### Result

- result_id: String — Required, unique
- game_id: String — Required, unique
- home_score: Integer — Required
- away_score: Integer — Required
- is_forfeit: Boolean — Required
- result_status: String — Required (Entered, Confirmed, Disputed)
- winner_team_id: String — Optional (empty for a tie)
- entered_by: String — Required
- entered_at: DateTime — Required

### Player stat

- stat_id: String — Required, unique
- game_id: String — Required
- player_id: String — Required
- did_not_play: Boolean — Required
- values: List of stat type and number — Required

### Stat type

- stat_type_id: String — Required, unique
- sport_id: String — Required
- name: String — Required

### Change history

- change_id: String — Required, unique
- record_type: String — Required (Result, Stat)
- record_id: String — Required
- changed_by: String — Required
- changed_at: DateTime — Required
- old_value: String — Required
- new_value: String — Required

-----

## Gherkin AC

### US-11.1 — Enter result

#### Scenario: Result is saved

- **Given** a manager's team played a finished game
- **When** the manager enters the score 21 to 14 and saves
- **Then** the system saves the result and the game shows Completed

#### Scenario: Result is not saved due to missing information

- **Given** a result is being entered
- **When** a score is missing
- **Then** the system does not save the result

#### Scenario: Manager cannot enter a result for another team's game

- **Given** a manager is signed in
- **When** the manager tries to enter a score for a game that does not include the manager's team
- **Then** the system rejects the change

#### Scenario: Wrong role cannot change results

- **Given** a ref is signed in
- **When** the ref tries to enter a result
- **Then** the system rejects the change

### US-11.2 — Enter player stats

#### Scenario: Player stats are saved

- **Given** John played in the game
- **When** the manager enters 12 points for John
- **Then** the system saves John's stats for that game

#### Scenario: Stats for a player outside the game are rejected

- **Given** a player is not on either team in the game
- **When** the manager tries to enter stats for that player
- **Then** the system rejects the stats

#### Scenario: Totals update

- **Given** John has 12 points in game 1
- **When** the manager enters 8 points for John in game 2
- **Then** John's season total is 20 points

### US-11.3 — Enter forfeit

#### Scenario: Forfeit is saved

- **Given** "Hawks" did not show up
- **When** the manager enters a forfeit for "Eagles"
- **Then** "Eagles" wins and the result shows Forfeit

### US-11.4 — Change my result within 48 hours

#### Scenario: Result is changed in time

- **Given** a manager entered a result 1 hour ago
- **When** the manager changes the score and saves
- **Then** the system saves the new score

#### Scenario: Change after 48 hours is rejected

- **Given** a manager entered a result 3 days ago
- **When** the manager tries to change it
- **Then** the system rejects the change and says that only the owner can change it now

### US-11.5 — Correct a result as owner

#### Scenario: Owner corrects an old result

- **Given** a result was entered 3 days ago
- **When** the owner changes the score and saves
- **Then** the system saves the new score

#### Scenario: Closed season needs reopening

- **Given** a season is Completed
- **When** the owner tries to change a result in it
- **Then** the system asks the owner to reopen the season first

### US-11.6 — See change history

#### Scenario: History is displayed

- **Given** the owner changed a score from 21-14 to 24-14
- **When** the owner opens the history
- **Then** the system shows who changed it, when, and the old and new score

### US-11.7 — Set stat types for a sport

#### Scenario: Stat types are saved

- **Given** a sport exists
- **When** the owner adds the stat types "points" and "rebounds" for basketball
- **Then** the system saves them

#### Scenario: Stat types are used

- **Given** basketball has the stat types "points" and "rebounds"
- **When** a manager enters stats for a basketball game
- **Then** the system asks for points and rebounds

### US-11.8 — Mark player did not play

#### Scenario: Player did not play

- **Given** John was absent
- **When** the manager marks John as "did not play"
- **Then** John gets no stats for that game

### US-11.9 — See games without a result

#### Scenario: Games without a result are listed

- **Given** 2 finished games of the team have no result
- **When** the manager opens the list
- **Then** the system shows those 2 games

### US-11.10 — Standings and leaders

#### Scenario: Standings update

- **Given** "Eagles" won 3 games and lost 1
- **When** a person opens the standings
- **Then** the system shows 3 wins and 1 loss for "Eagles"

#### Scenario: Box score is displayed

- **Given** a game has a result and stats
- **When** a person opens the game
- **Then** the system shows the score and the stats of each player

#### Scenario: Leaders are displayed

- **Given** players have stats in the season
- **When** a person opens the leaders page
- **Then** the system shows the top scorers in order

### US-11.11 — Confirm or dispute a result

#### Scenario: Result is confirmed

- **Given** the manager of "Eagles" entered the score 21 to 14
- **When** the manager of "Hawks" confirms it
- **Then** the result shows Confirmed

#### Scenario: Result is disputed

- **Given** the manager of "Eagles" entered the score 21 to 14
- **When** the manager of "Hawks" disputes it
- **Then** the result shows Disputed
- **And** the owner sees it in a list to decide

#### Scenario: Owner decides a disputed result

- **Given** a result is Disputed
- **When** the owner enters the final score
- **Then** the result shows Confirmed
- **And** the history keeps who decided

#### Scenario: Second result for the same game is rejected

- **Given** a game already has a result
- **When** the other manager tries to enter a different score as a new result
- **Then** the system rejects the new result and offers to dispute the existing one
