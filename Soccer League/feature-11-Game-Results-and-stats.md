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
