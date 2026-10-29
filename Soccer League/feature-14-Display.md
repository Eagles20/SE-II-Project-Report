# Feature: Display

**Feature ID:** 14  
**Branch pattern:** `feature/14-display`  
**Status:** Draft  
**Created:** 2026-10-21  
**Input:** Show leagues, seasons, schedules, standings, teams, players and stats to the public.  
**Depends on:** [Feature 2-Maintain-Sport](Feature-2-Maintain-Sport.md), [Feature 3-Maintain-League](Feature-3-Maintain-League.md), [Feature 4-Maintain-Season](Feature-4-Maintain-Season.md), [Feature 5-Maintain-Game](Feature-5-Maintain-Game.md), [Feature 6-Maintain-Team](Feature-6-Maintain-Team.md), [Feature 7-Maintain-Player](Feature-7-Maintain-Playermd), [Feature 11-Game-Results-and-Stats](Feature-11-Game-Results-and-Stats.md)

------

## User Stories

### US-14.1: View the home page

**As a** person from the public  
**I want to** see upcoming games and recent results on the home page  
**So that** I see what is new without searching.  
**Priority:** P1  
**Independent test:** Open the home page and verify that games, results and announcements are shown.  
**Acceptance Scenarios:** see ### US-14.1 under Gherkin AC

### US-14.2: Browse sports, leagues and seasons

**As a** person from the public  
**I want to** browse Sport, then League, then Season  
**So that** I can reach what I need step by step.  
**Priority:** P1  
**Independent test:** Click from a sport to a season and verify the pages.  
**Acceptance Scenarios:** see ### US-14.2 under Gherkin AC

### US-14.3: View and filter the schedule

**As a** person from the public  
**I want to** see the schedule of a season and filter it by team, date or location  
**So that** I can plan to watch.  
**Priority:** P1  
**Independent test:** Filter a schedule by team and verify the result.  
**Acceptance Scenarios:** see ### US-14.3 under Gherkin AC

### US-14.4: View standings

**As a** person from the public  
**I want to** see the standings of a season  
**So that** I know who is leading.  
**Priority:** P1  
**Independent test:** Open the standings and verify that they match the results.  
**Acceptance Scenarios:** see ### US-14.4 under Gherkin AC

### US-14.5: View a team page

**As a** family member or friend  
**I want to** open a team page with players, games and record  
**So that** I can follow the team.  
**Priority:** P1  
**Independent test:** Open a team page and verify its content.  
**Acceptance Scenarios:** see ### US-14.5 under Gherkin AC

### US-14.6: View a player page

**As a** family member or friend  
**I want to** open a player page with stats for each game and the season total  
**So that** I can see how the player plays.  
**Priority:** P1  
**Independent test:** Open a player page and verify the stats.  
**Acceptance Scenarios:** see ### US-14.6 under Gherkin AC

### US-14.7: View a game page

**As a** person from the public  
**I want to** open a game page with the result and player stats  
**So that** all game information is in one place.  
**Priority:** P2  
**Independent test:** Open a finished game and verify the content.  
**Acceptance Scenarios:** see ### US-14.7 under Gherkin AC

### US-14.8: View leaders

**As a** person from the public  
**I want to** see the leaders of a league  
**So that** I can follow the best players.  
**Priority:** P2  
**Independent test:** Open the leaders page and verify the order.  
**Acceptance Scenarios:** see ### US-14.8 under Gherkin AC

### US-14.9: Search teams and players

**As a** person from the public  
**I want to** search teams and players by name  
**So that** I find my team or my child fast.  
**Priority:** P2  
**Independent test:** Search a name and verify the result.  
**Acceptance Scenarios:** see ### US-14.9 under Gherkin AC

### US-14.10: Post announcements

**As an** owner  
**I want to** post announcements and sponsor messages on the home page  
**So that** the league can advertise and share news.  
**Priority:** P2  
**Independent test:** Post an announcement and verify that it is shown.  
**Acceptance Scenarios:** see ### US-14.10 under Gherkin AC

### US-14.11: Hide a league or season

**As an** owner  
**I want to** hide a league or a season from the public  
**So that** something that is not ready stays private.  
**Priority:** P2  
**Independent test:** Hide a league and verify that the public cannot see it.  
**Acceptance Scenarios:** see ### US-14.11 under Gherkin AC

### US-14.12: Share and print

**As a** person from the public  
**I want to** copy the link of a page and print the schedule  
**So that** I can share with family and keep a paper copy.  
**Priority:** P3  
**Independent test:** Copy a team page link and open it on another phone.  
**Acceptance Scenarios:** see ### US-14.12 under Gherkin AC

-----

## Functional Requirements

- **FR-001:** The system MUST have public pages that need no login.
- **FR-002:** The public home page MUST show upcoming games, recent results and announcements.
- **FR-003:** The system MUST let the public browse Sport, then League, then Season.
- **FR-004:** The system MUST show the schedule of a season and MUST let the public filter it by team, date and location.
- **FR-005:** The system MUST show the standings of each season (wins, losses, ties).
- **FR-006:** The system MUST have a team page (players, games, record), a player page (stats for each game and season total) and a game page (teams, date, time, location, result, player stats).
- **FR-007:** The system MUST show leaders (for example top scorers) for each league.
- **FR-008:** The system MUST let the public search teams and players by name.
- **FR-009:** The system MUST show cancelled and moved games with the reason.
- **FR-010:** The system MUST show "Result under review" instead of the score when a result is Disputed.
- **FR-011:** Each game, team and player page MUST have its own link that can be shared, and the schedule MUST have a print-friendly view.
- **FR-012:** The system MUST let the owner post announcements and sponsor messages on the home page.
- **FR-013:** The system MUST let the owner hide a league or a season from the public.
- **FR-014:** The system MUST NOT show emails, phone numbers or ref pay on any public page.
- **FR-015:** The system MUST keep past seasons visible.
- **FR-016:** When there is nothing to show (no games, no results, no players), a public page MUST show a clear message such as "No games yet" and MUST NOT show an error or an empty table.
- **FR-017:** When a filter or search finds nothing, the page MUST show "Nothing found" and a way to clear the filter. A date filter MUST include both the start day and the end day.
- **FR-018:** The system MUST let the owner manage announcements and visibility (main user: public viewer), and MUST NOT let managers, refs or the public change them.
- **FR-019:** The system MUST work well on a phone.

-----

## Screen Requirements

### SCR-14.1: Public home page

- **Who can open it:** Everyone (no login needed)
- **Content:** Upcoming games, recent results, and the active announcements and sponsor messages
- **Fields:** Search box (search teams and players by name)
- **Buttons and links:** Open a game, Open a team, Browse sports, Staff login
- **Rules:**
  - Show upcoming games, recent results and announcements (FR-002).
  - Show an announcement only between its start date and its end date.
  - If there are no games or results, show a clear message such as "No games yet" (FR-016).
  - Do not show any edit buttons.
- **Related:** US-14.1, FR-001, FR-002, FR-016

### SCR-14.2: Browse sports, leagues and seasons page

- **Who can open it:** Everyone (no login needed)
- **Content:** Three levels. First a list of sports, then the leagues of the chosen sport, then the seasons of the chosen league.
- **Buttons and links:** Open a sport, Open a league, Open a season, Back
- **Rules:**
  - The public browses Sport, then League, then Season (FR-003).
  - Do not show a league or a season that the owner hid (FR-013).
  - Past seasons stay in the list (FR-015).
  - If a level has nothing to show, show a clear message (FR-016).
- **Related:** US-14.2, FR-003, FR-013, FR-015, FR-016

### SCR-14.3: Season schedule page

- **Who can open it:** Everyone (no login needed)
- **Fields:** Filters: Team, Start date, End date, Location
- **Content:** A table of the games of the season with these columns: Date, Time, Home team, Away team, Location, Status. A cancelled or moved game shows the reason.
- **Buttons and links:** Clear filters, Print view, Copy link, Open a game
- **Rules:**
  - The public can filter the schedule by team, date and location (FR-004).
  - A date filter includes both the start day and the end day (FR-017).
  - Show cancelled and moved games with the reason (FR-009).
  - If the season has no games, show "No games yet" (FR-016).
  - If a filter finds nothing, show "Nothing found" and a way to clear the filter (FR-017).
  - Show only published games.
- **Related:** US-14.3, US-14.12, FR-004, FR-009, FR-016, FR-017

### SCR-14.4: Print schedule view

- **Who can open it:** Everyone (no login needed)
- **Content:** The schedule of the season in a layout that fits on paper
- **Buttons and links:** Print, Back to schedule
- **Rules:**
  - The schedule has a print-friendly view (FR-011).
  - Do not show menus or buttons that are not needed on paper.
- **Related:** US-14.12, FR-011

### SCR-14.5: Standings page

- **Who can open it:** Everyone (no login needed)
- **Content:** A table of the teams of a season with these columns: Team, Wins, Losses, Ties
- **Buttons and links:** Open a team
- **Rules:**
  - Show the standings of the season, built from the results (FR-005).
  - If a season has no results, show all teams with 0 wins, 0 losses and 0 ties.
- **Related:** US-14.4, FR-005

### SCR-14.6: Team page

- **Who can open it:** Everyone (no login needed)
- **Content:** The team name, the players, the games and the record (wins, losses, ties)
- **Buttons and links:** Open a player, Open a game, Copy link
- **Rules:**
  - The page has its own link that can be shared (FR-011).
  - Do not show the email or the phone of any player (FR-014).
  - If the team has no players or no games, show a clear message (FR-016).
- **Related:** US-14.5, US-14.12, FR-006, FR-011, FR-014, FR-016

### SCR-14.7: Player page

- **Who can open it:** Everyone (no login needed)
- **Content:** The player name, team, the stats for each game, and the season total
- **Buttons and links:** Open a game, Open the team, Copy link
- **Rules:**
  - The page has its own link that can be shared (FR-011).
  - Do not show the email or the phone of the player (FR-014).
  - If the player has no stats, show a clear message (FR-016).
- **Related:** US-14.6, US-14.12, FR-006, FR-011, FR-014, FR-016

### SCR-14.8: Game page

- **Who can open it:** Everyone (no login needed)
- **Content:** The teams, date, time, location (with address and map link), the result, and the stats of each player
- **Buttons and links:** Open a team, Open a player, Copy link
- **Rules:**
  - The page has its own link that can be shared (FR-011).
  - When the result is Disputed, show "Result under review" and no score (FR-010).
  - A cancelled or moved game shows the reason (FR-009).
  - If the game has no result yet, show a clear message (FR-016).
  - Do not show ref pay (FR-014).
- **Related:** US-14.7, US-14.12, FR-006, FR-009, FR-010, FR-011, FR-014, FR-016

### SCR-14.9: Leaders page

- **Who can open it:** Everyone (no login needed)
- **Content:** The leaders of a league for each stat type, for example the top scorers in order
- **Buttons and links:** Open a player
- **Rules:**
  - Show the leaders for each league (FR-007).
  - If there are no stats yet, show a clear message (FR-016).
- **Related:** US-14.8, FR-007, FR-016

### SCR-14.10: Search page

- **Who can open it:** Everyone (no login needed)
- **Fields:** Search box (search by name)
- **Content:** A list of matching teams and a list of matching players
- **Buttons and links:** Open a team, Open a player, Clear search
- **Rules:**
  - Search finds teams and players by part of the name (FR-008).
  - If nothing is found, show "Nothing found" and a way to clear the search (FR-017).
  - Do not show the email or the phone of any player (FR-014).
- **Related:** US-14.9, FR-008, FR-014, FR-017

### SCR-14.11: Manage announcements page

- **Who can open it:** Owner only
- **Content:** A list of announcements with these columns: Title, Start date, End date, Record state
- **Fields:** Title (required), Message (required), Start date (required), End date (optional)
- **Buttons and links:** Add announcement, Edit, Make inactive / Make active, Delete, Save, Cancel
- **Rules:**
  - The owner can post announcements and sponsor messages for the home page (FR-012).
  - If a required field is empty, do not save the announcement.
  - Managers, refs and the public cannot open this page (FR-018).
- **Related:** US-14.10, FR-012, FR-018

### SCR-14.12: Manage visibility page

- **Who can open it:** Owner only
- **Content:** A list of the leagues and seasons with these columns: Name, Type (League or Season), Visible to the public (Yes or No)
- **Buttons and links:** Hide, Show
- **Rules:**
  - The owner can hide a league or a season from the public (FR-013).
  - A hidden league or season does not appear on any public page. All data stays in the system.
  - Managers, refs and the public cannot open this page (FR-018).
- **Related:** US-14.11, FR-013, FR-018

### Rules for all screens

- Every public screen MUST work well on a phone (FR-019).
- Public screens need no login and show no edit buttons (FR-001).
- Public screens MUST NOT show emails, phone numbers or ref pay (FR-014).
- Past seasons MUST stay visible (FR-015).
- Error messages MUST be short and clear. A page with nothing to show uses a clear message, not an error (FR-016).

-----

## Key Entities

- **Public page** — A page that anyone can open without login.
- **Announcement** — A message from the owner shown on the home page.

-----

## Initial Data Model

### Announcement

- announcement_id: String — Required, unique
- title: String — Required
- message: String — Required
- start_date: Date — Required
- end_date: Date — Optional
- record_state: String — Required (Active, Inactive, Deleted). Deleted is a soft delete, see shared/GLOSSARY.md

### Public visibility

- record_type: String — Required (League, Season)
- record_id: String — Required
- is_public: Boolean — Required

-----

## Gherkin AC

### US-14.1 — View the home page

#### Scenario: Home page is displayed

- **Given** there are games this week
- **When** a person who is not logged in opens the home page
- **Then** the system shows upcoming games and recent results

#### Scenario: Public cannot change data

- **Given** a person is not logged in
- **When** the person opens any public page
- **Then** the system shows no edit buttons

### US-14.2 — Browse sports, leagues and seasons

#### Scenario: Browse to a season

- **Given** sports, leagues and seasons exist
- **When** the person opens a sport, then a league, then a season
- **Then** the system shows the season page

### US-14.3 — View and filter the schedule

#### Scenario: Schedule is displayed

- **Given** a season has published games
- **When** the person opens the season schedule
- **Then** the system shows the games with date, time and location

#### Scenario: Filter by team

- **Given** the schedule has games of several teams
- **When** the person filters by "Eagles"
- **Then** the system shows only games with "Eagles"

#### Scenario: Nothing found

- **Given** the schedule has no games for "Eagles"
- **When** the person filters by "Eagles"
- **Then** the system shows "Nothing found" and a way to clear the filter

#### Scenario: Season with no games yet

- **Given** a season has no games
- **When** the person opens the schedule
- **Then** the system shows "No games yet"

#### Scenario: Cancelled game shows the reason

- **Given** a game was cancelled with the reason "Rain"
- **When** the person opens the schedule
- **Then** the system shows Cancelled and the reason

### US-14.4 — View standings

#### Scenario: Standings are displayed

- **Given** results exist for a season
- **When** the person opens the standings
- **Then** the system shows wins, losses and ties for each team

#### Scenario: No results yet

- **Given** a season has no results
- **When** the person opens the standings
- **Then** the system shows all teams with 0 wins, 0 losses and 0 ties

### US-14.5 — View a team page

#### Scenario: Team page is displayed

- **Given** a team exists
- **When** the person opens the team page
- **Then** the system shows the players, the games and the record

### US-14.6 — View a player page

#### Scenario: Player page is displayed

- **Given** John played 3 games
- **When** the person opens John's page
- **Then** the system shows his stats for each game and the season total

#### Scenario: Private data is hidden

- **Given** a player has an email and a phone
- **When** the person opens the player page
- **Then** the system does not show the email or the phone

### US-14.7 — View a game page

#### Scenario: Game page is displayed

- **Given** a game has a result
- **When** the person opens the game page
- **Then** the system shows teams, date, time, location, score and player stats

#### Scenario: Disputed result is not shown

- **Given** a result is Disputed
- **When** the person opens the game page
- **Then** the page shows "Result under review" and no score

### US-14.8 — View leaders

#### Scenario: Leaders are displayed

- **Given** players have stats in the league
- **When** the person opens the leaders page
- **Then** the system shows the top players in order

### US-14.9 — Search teams and players

#### Scenario: Search finds a team

- **Given** teams exist
- **When** the person searches for part of a team name
- **Then** the system shows the matching teams

#### Scenario: Search finds a player

- **Given** players exist
- **When** the person searches for part of a player name
- **Then** the system shows the matching players

### US-14.10 — Post announcements

#### Scenario: Announcement is displayed

- **Given** the owner posted "Registration opens Monday"
- **When** the public opens the home page
- **Then** the announcement is shown

#### Scenario: Wrong role cannot post

- **Given** a manager is signed in
- **When** the manager tries to post an announcement
- **Then** the system rejects the action

### US-14.11 — Hide a league or season

#### Scenario: League is hidden

- **Given** the owner hid "Fall League"
- **When** the public opens the league list
- **Then** "Fall League" is not shown

### US-14.12 — Share and print

#### Scenario: Shared link opens the same page

- **Given** a person is on a team page
- **When** the person copies the link and opens it on another phone
- **Then** the same team page opens

#### Scenario: Print view is displayed

- **Given** a schedule is shown
- **When** the person opens the print view
- **Then** the system shows a schedule that fits on paper
