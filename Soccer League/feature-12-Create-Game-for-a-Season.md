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

## Screen Requirements

### SCR-12.1: Season schedule page

- **Who can open it:** Owner only
- **Fields:** Season (required, choose a season)
- **Content:** The schedule of the chosen season: status (No schedule, Draft or Published), and when it was generated or published
- **Buttons and links:** Set settings, Generate schedule, View preview, View summary, Publish, Delete schedule, View history
- **Rules:**
  - The owner chooses a season and starts "Generate schedule" (FR-001).
  - A season can have only one generated schedule (Draft or Published). If the season already has one, ask the owner to replace or delete it first (FR-015).
  - Other roles cannot open this page (FR-019).
- **Related:** US-12.2, US-12.6, US-12.7, FR-001, FR-015, FR-019

### SCR-12.2: Generator settings page

- **Who can open it:** Owner only
- **Fields:** Season (required), Play days and times (required), Locations and fields (required, choose one or more), Refs (required, choose the refs who are available)
- **Buttons and links:** Save settings, Generate schedule, Cancel
- **Rules:**
  - If a required field is empty, for example no location is chosen, do not save the settings (FR-002).
  - Show only active locations and active refs.
  - The system creates games so that each active team plays the number of games set in the league (FR-004).
- **Related:** US-12.1, US-12.2, FR-002, FR-004

### SCR-12.3: Team blackout dates page

- **Who can open it:** Owner only
- **Fields:** Team (required), Date (required)
- **Content:** The list of blackout dates of the teams
- **Buttons and links:** Add blackout date, Back
- **Rules:**
  - A team has no game on its blackout dates (FR-003).
- **Related:** US-12.3, FR-003

### SCR-12.4: Schedule preview page

- **Who can open it:** Owner only
- **Content:** A table of the generated games with these columns: Date, Time, Home team, Away team, Location, Field, Ref. Below it, a list of problems that the system could not solve (for example not enough refs or time slots).
- **Buttons and links:** Edit game, Save as draft, View summary, Back
- **Rules:**
  - Show the preview before anything is saved. Nothing is saved until the owner confirms (FR-010, FR-017).
  - List the problems, for example the games without a ref (FR-010).
  - A game without a ref is marked Needs ref (FR-016).
  - No team, field or ref is in two games at the same time (FR-008).
  - Teams play different opponents as much as possible, and home and away games are balanced (FR-005, FR-006).
- **Related:** US-12.2, US-12.4, FR-005, FR-006, FR-007, FR-008, FR-010, FR-016, FR-017

### SCR-12.5: Edit game in preview page

- **Who can open it:** Owner only
- **Fields:** Date (required), Time (required), Location and field (required), Ref (required)
- **Buttons and links:** Save change, Cancel
- **Rules:**
  - Show the current information of the game when the page opens.
  - After saving, the preview shows the change and keeps the other games (FR-011).
  - Do not put a team, a field or a ref in two games at the same time (FR-008).
- **Related:** US-12.5, FR-008, FR-011

### SCR-12.6: Schedule summary page

- **Who can open it:** Owner only
- **Content:** Three tables: Games per team, Games per location, Games per ref
- **Buttons and links:** Back
- **Rules:**
  - Show the summary for the generated schedule (FR-012).
  - The owner uses it to check that the games are shared fairly, including between refs (FR-009).
- **Related:** US-12.8, FR-009, FR-012

### SCR-12.7: Confirm save or publish message

- **Who can open it:** Owner only (shown after the owner clicks Save as draft or Publish)
- **Content:** A short question such as "Do you want to save this schedule as a draft?" or "Do you want to publish this schedule?". If some games are marked Needs ref, show a warning with the number of those games.
- **Buttons and links:** Confirm, Cancel
- **Rules:**
  - Nothing is saved or published until the owner clicks Confirm (FR-017).
  - Saving creates a Draft. Managers and the public do not see a Draft (FR-013).
  - Publishing is allowed with Needs ref games, but only after the warning is shown and the owner confirms (FR-016).
  - Save the action in the schedule history (FR-018).
- **Related:** US-12.4, US-12.6, FR-013, FR-016, FR-017, FR-018

### SCR-12.8: Delete schedule confirm message

- **Who can open it:** Owner only (shown after the owner clicks Delete schedule)
- **Content:** The season name and a question such as "Do you want to delete this generated schedule?"
- **Buttons and links:** Confirm delete, Cancel
- **Rules:**
  - If any game of the schedule has a result, reject the delete. The games stay unchanged (FR-014).
  - If no game has a result, remove the generated games.
  - Save the action in the schedule history (FR-018).
- **Related:** US-12.7, FR-014, FR-018

### SCR-12.9: Schedule history page

- **Who can open it:** Owner only
- **Content:** A table of the history of the schedule. Each row shows the action (Generated, Published or Deleted), who did it and when.
- **Buttons and links:** Back
- **Rules:**
  - Show who did each action and when (FR-018).
- **Related:** FR-018

### SCR-12.10: Published schedule page (manager)

- **Who can open it:** Manager (login needed)
- **Content:** A table of the games of the manager's team with these columns: Date, Time, Opponent, Home or away, Location
- **Rules:**
  - Show the games only after the owner publishes the schedule (FR-013).
  - A manager sees only the games of their own team.
  - The page is read only. Do not show any edit buttons.
  - The public sees the published games on the public schedule page.
- **Related:** US-12.9, FR-013

### Rules for all screens

- Every screen MUST work on an office computer (FR-020).
- Only the owner can generate, save, publish or delete a schedule. Other roles MUST be rejected (FR-019).
- Error messages MUST be short and clear.

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
