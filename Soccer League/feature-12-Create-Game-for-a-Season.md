# Feature: Create Games for a Season

**Feature ID:** 12  
**Branch pattern:** `feature/12-create-games-for-a-season`  
**Status:** Draft  
**Created:** 2026-10-21  
**Input:** Generate the games of a season (teams, dates, times, locations and refs) so that the owner does not make the schedule by hand.  
**Depends on:** [Feature 4-Maintain-Season](Feature-4-Maintain-Season.md), [Feature 5-Maintain-Game](Feature-5-Maintain-Game.md), [Feature 6-Maintain-Team](Feature-6-Maintain-Team.md), [Feature 8-Maintain-Location](Feature-8-Maintain-Location.md), [Feature 9-Maintain-Ref](Feature-9-Maintain-Ref.md)

------

## User Stories

### US-12.1: Set generator settings

**As an** owner  
**I want to** choose the days, times, locations and refs for a season  
**So that** the schedule fits our weekends and evenings.  
**Priority:** P1  
**Independent test:** Set the options and verify that they are saved.  
**Acceptance Scenarios:** see ### US-12.1 under Gherkin AC

### US-12.2: Generate a draft schedule

**As an** owner  
**I want to** generate the games of a season  
**So that** I do not make the schedule by hand.  
**Priority:** P1  
**Independent test:** Generate a schedule and verify that every team has the right number of games.  
**Acceptance Scenarios:** see ### US-12.2 under Gherkin AC

### US-12.3: Enter team blackout dates

**As an** owner  
**I want to** enter dates when a team cannot play  
**So that** the system does not put a game on those days.  
**Priority:** P2  
**Independent test:** Add a blackout date and verify that the team has no game on it.  
**Acceptance Scenarios:** see ### US-12.3 under Gherkin AC

### US-12.4: Preview and see problems

**As an** owner  
**I want to** see a preview and a list of problems before saving  
**So that** I know what to fix.  
**Priority:** P1  
**Independent test:** Generate with no refs and verify that the problem is listed.  
**Acceptance Scenarios:** see ### US-12.4 under Gherkin AC

### US-12.5: Edit a game in the preview

**As an** owner  
**I want to** edit one game in the preview  
**So that** I can fix small things without starting over.  
**Priority:** P2  
**Independent test:** Change a game time in the preview and verify that it is kept.  
**Acceptance Scenarios:** see ### US-12.5 under Gherkin AC

### US-12.6: Save as draft and publish

**As an** owner  
**I want to** save the schedule as a draft and publish it later  
**So that** managers and the public see it only when I am ready.  
**Priority:** P1  
**Independent test:** Publish a draft and verify that the public can see the games.  
**Acceptance Scenarios:** see ### US-12.6 under Gherkin AC

### US-12.7: Generate again or delete the schedule

**As an** owner  
**I want to** generate again with new settings or delete a generated schedule  
**So that** I can try other options.  
**Priority:** P2  
**Independent test:** Delete a draft schedule and verify that the games are removed.  
**Acceptance Scenarios:** see ### US-12.7 under Gherkin AC

### US-12.8: See the schedule summary

**As an** owner  
**I want to** see games per team, per location and per ref  
**So that** I can check that the schedule is fair.  
**Priority:** P2  
**Independent test:** Generate a schedule and verify that the summary is shown.  
**Acceptance Scenarios:** see ### US-12.8 under Gherkin AC

### US-12.9: View the published schedule

**As a** manager  
**I want to** see my team's schedule when it is published  
**So that** I can plan with my players.  
**Priority:** P1  
**Independent test:** Publish a schedule and verify that the manager sees the team games.  
**Acceptance Scenarios:** see ### US-12.9 under Gherkin AC

-----

## Functional Requirements

- **FR-001:** The system MUST let the owner choose a season and start "Generate schedule".
- **FR-002:** The system MUST let the owner choose the days and times when games can be played, the locations and fields to use, and the refs who are available.
- **FR-003:** The system MUST let the owner enter blackout dates for a team, and MUST NOT put a game for that team on those dates.
- **FR-004:** The system MUST create games so that each active team plays the number of games set in the league.
- **FR-005:** The system MUST make teams play different opponents (round robin) as much as possible.
- **FR-006:** The system MUST balance home and away games for each team.
- **FR-007:** The system MUST give every game a date, a time, a location, a field and at least one ref.
- **FR-008:** The system MUST NOT put a team, a field or a ref in two games at the same time.
- **FR-009:** The system MUST share the games fairly between refs.
- **FR-010:** The system MUST show a preview before anything is saved, and MUST list the problems it could not solve (for example not enough refs or time slots).
- **FR-011:** The system MUST let the owner edit one game in the preview.
- **FR-012:** The system MUST show a summary: games per team, per location and per ref.
- **FR-013:** The generated schedule MUST be saved as a Draft. Managers and the public MUST see it only after the owner publishes it.
- **FR-014:** The system MUST let the owner generate again or delete a whole generated schedule only if no game has a result.
- **FR-015:** The system MUST allow only one generated schedule (Draft or Published) for a season at a time.
- **FR-016:** The system MUST let the owner save a schedule that has games marked Needs ref, and MUST warn the owner before publishing it.
- **FR-017:** The system MUST ask the owner to confirm before saving or publishing the schedule.
- **FR-018:** The system MUST keep a history of the schedule (generated, published, deleted) with who and when.
- **FR-019:** The system MUST let the owner use this feature (main user: owner), and MUST NOT let other roles generate a schedule.
- **FR-020:** The system MUST work on an office computer.

-----

## Key Entities

- **Schedule** — The set of generated games of one season.
- **Schedule settings** — The days, times, locations, refs and blackout dates chosen by the owner.
- **Schedule history** — The record of who generated, published or deleted a schedule.
- **Blackout date** — A date when a team cannot play.

-----

## Initial Data Model

### Schedule

- schedule_id: String — Required, unique
- season_id: String — Required
- status: String — Required (Draft, Published)
- created_at: DateTime — Required
- published_at: DateTime — Optional

### Schedule settings

- settings_id: String — Required, unique
- schedule_id: String — Required
- play_days_and_times: List — Required
- location_ids: List — Required
- ref_ids: List — Required

### Blackout date

- blackout_id: String — Required, unique
- team_id: String — Required
- blackout_date: Date — Required

### Schedule history

- history_id: String — Required, unique
- schedule_id: String — Required
- action: String — Required (Generated, Published, Deleted)
- changed_by: String — Required
- changed_at: DateTime — Required

-----

## Gherkin AC

### US-12.1 — Set generator settings

#### Scenario: Settings are saved

- **Given** a season exists
- **When** the owner chooses play days, locations and refs and saves
- **Then** the system saves the settings

#### Scenario: Settings are not saved due to missing information

- **Given** settings are being entered
- **When** no location is chosen
- **Then** the system does not save the settings

#### Scenario: Wrong role cannot generate a schedule

- **Given** a manager is signed in
- **When** the manager tries to generate a schedule
- **Then** the system rejects the action

### US-12.2 — Generate a draft schedule

#### Scenario: Schedule is generated

- **Given** "Fall League" has 6 teams, 3 locations and 4 refs
- **When** the owner generates the schedule for "Fall 2026"
- **Then** every team has 10 games
- **And** every game has a location and a ref

#### Scenario: Teams meet different opponents

- **Given** a schedule is generated
- **When** the owner opens a team's games
- **Then** the team plays different opponents as much as possible

#### Scenario: Home and away are balanced

- **Given** each team plays 10 games
- **When** the schedule is generated
- **Then** each team has 5 home games and 5 away games, or as close as possible

#### Scenario: No double booking

- **Given** a schedule is generated
- **When** the owner checks the games
- **Then** no team, field or ref is in two games at the same time

### US-12.3 — Enter team blackout dates

#### Scenario: Blackout date is respected

- **Given** "Eagles" cannot play on Nov 8
- **When** the owner generates the schedule
- **Then** "Eagles" has no game on Nov 8

### US-12.4 — Preview and see problems

#### Scenario: Problems are listed

- **Given** there are no refs in the system
- **When** the owner generates the schedule
- **Then** the system shows that games need refs and lists the games without a ref

#### Scenario: Nothing is saved before confirmation

- **Given** a schedule was generated
- **When** the owner does not confirm
- **Then** no games are saved

#### Scenario: Schedule with games that need a ref

- **Given** 2 games have no ref
- **When** the owner publishes the schedule
- **Then** the system warns about the 2 games and publishes only after the owner confirms

### US-12.5 — Edit a game in the preview

#### Scenario: Game is edited in the preview

- **Given** a preview is shown
- **When** the owner changes the time of one game
- **Then** the preview shows the new time and keeps the other games

### US-12.6 — Save as draft and publish

#### Scenario: Draft is not public

- **Given** the owner generated a schedule and did not publish it
- **When** the public opens the season
- **Then** the generated games are not shown

#### Scenario: Schedule is published

- **Given** a draft schedule is ready
- **When** the owner confirms and publishes it
- **Then** managers and the public can see the games

### US-12.7 — Generate again or delete the schedule

#### Scenario: Draft schedule is deleted

- **Given** a schedule has no results
- **When** the owner deletes it
- **Then** the generated games are removed

#### Scenario: Schedule with results cannot be deleted

- **Given** one game already has a result
- **When** the owner tries to delete the generated schedule
- **Then** the system rejects the delete operation
- **And** the games stay unchanged

#### Scenario: Second schedule for the same season is rejected

- **Given** "Fall 2026" already has a Draft schedule
- **When** the owner starts another generation for "Fall 2026"
- **Then** the system asks the owner to replace or delete the existing schedule first

### US-12.8 — See the schedule summary

#### Scenario: Summary is displayed

- **Given** a schedule is generated
- **When** the owner opens the summary
- **Then** the system shows the games per team, per location and per ref

### US-12.9 — View the published schedule

#### Scenario: Manager sees the published schedule

- **Given** a schedule is published
- **When** a manager opens the schedule
- **Then** the system shows the games of the manager's team
