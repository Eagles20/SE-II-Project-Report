# Feature: Maintain Season

**Feature ID:** 4  
**Branch pattern:** `feature/4-maintain-season`  
**Status:** Draft  
**Created:** 2026-10-19
**Input:** Maintain seasons  for a league.  
**Depends on:** [Feature 3 — Maintain-League](feature-2-Maintain-League.md)


------

## User Stories

### US-4.1: Add season

**As an** owner  
**I want to** add a season to a league  
**So that** games can be scheduled in it.  
**Priority:** P1  
**Independent test:** Add a season and verify that it is saved.  
**Acceptance Scenarios:** see ### US-4.1 under Gherkin AC

### US-4.2: Edit season dates

**As an** owner  
**I want to** edit the season name and dates  
**So that** the plan can change.  
**Priority:** P1  
**Independent test:** Edit a season and verify that the change is saved.  
**Acceptance Scenarios:** see ### US-4.2 under Gherkin AC

### US-4.3: Delete season

**As an** owner  
**I want to** delete a season  
**So that** a season made by mistake can be removed.  
**Priority:** P1  
**Independent test:** Delete a season and verify that it is no longer active.  
**Acceptance Scenarios:** see ### US-4.3 under Gherkin AC

### US-4.4: View season summary

**As an** owner  
**I want to** view a season with a summary  
**So that** I can see the progress at a glance.  
**Priority:** P1  
**Independent test:** Open a season and verify the summary numbers.  
**Acceptance Scenarios:** see ### US-4.4 under Gherkin AC

### US-4.5: Change season status

**As an** owner  
**I want to** set the season status to Planned, In Progress or Completed  
**So that** everyone knows where the season is.  
**Priority:** P2  
**Independent test:** Change the status and verify that it is shown.  
**Acceptance Scenarios:** see ### US-4.5 under Gherkin AC

### US-4.6: Close season

**As an** owner  
**I want to** close a season  
**So that** managers cannot change results after the season ends.  
**Priority:** P2  
**Independent test:** Close a season and verify that managers cannot change results.  
**Acceptance Scenarios:** see ### US-4.6 under Gherkin AC

### US-4.7: Reopen season

**As an** owner  
**I want to** reopen a closed season  
**So that** I can fix a mistake in old records.  
**Priority:** P3  
**Independent test:** Reopen a season and verify that results can be changed.  
**Acceptance Scenarios:** see ### US-4.7 under Gherkin AC

### US-4.8: Public views seasons

**As a** person from the public  
**I want to** see the current season first and open past seasons  
**So that** I can find new games and old results.  
**Priority:** P2  
**Independent test:** Open a league page and verify that current and past seasons are shown.  
**Acceptance Scenarios:** see ### US-4.8 under Gherkin AC

-----

## Functional Requirements

- **FR-001:** The system MUST maintain seasons.
- **FR-002:** Each season MUST have a unique identifier.
- **FR-003:** The system MUST allow authorized users to add seasons.
- **FR-004:** The system MUST allow authorized users to edit seasons.
- **FR-005:** The system MUST allow authorized users to delete seasons.
- **FR-006:** The system MUST allow authorized users to view seasons.
- **FR-007:** Required season information MUST be provided before the season can be saved (name, league, start date, end date).
- **FR-008:** Every season MUST belong to one league.
- **FR-009:** The end date MUST be after the start date.
- **FR-010:** The system MUST reject a season whose dates overlap another season of the same league.
- **FR-011:** The system MUST NOT change season dates if a game would be outside the new dates.
- **FR-012:** A season MUST have a status: Planned, In Progress or Completed.
- **FR-013:** A Completed season MUST be locked. Managers MUST NOT change its results. Only the owner can reopen it.
- **FR-014:** The system MUST NOT delete a season that has games.
- **FR-015:** Deleting a season MUST be a soft delete (record state Deleted), so other features keep the original season information.
- **FR-016:** The system MUST show a season summary: total games, games played, games left.
- **FR-017:** The system MUST keep old seasons so that past records can be viewed.
- **FR-018:** The system MUST let the owner use this feature (main user: owner), and MUST NOT let other roles change its information.
- **FR-019:** The system MUST work on an office computer and on a phone.
- **FR-020:** This feature is not used very often, so the system MUST ask the user to confirm before saving a change.

-----

## Screen Requirements

### SCR-4.1: Season list page

- **Who can open it:** Owner only
- **Content:** A table of seasons with these columns: Name, League, Start date, End date, Status, Record state
- **Fields:** League filter (choose a league or All leagues)
- **Buttons and links:** Add season, View, Edit, Delete
- **Rules:**
  - When the owner chooses a league, show only the seasons of that league.
  - Seasons with the state Deleted are not shown in the list.
  - Other roles cannot open this page (FR-018).
- **Related:** US-4.4, US-4.5, FR-006, FR-012, FR-018

### SCR-4.2: Add season page

- **Who can open it:** Owner only
- **Fields:** League (required), Name (required), Start date (required), End date (required)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - If a required field is empty, do not save and show which field is missing (FR-007).
  - The end date must be after the start date (FR-009).
  - Reject a season whose dates overlap another season of the same league (FR-010).
  - When the owner clicks Save, show a confirm message before saving (FR-020).
  - A new season starts with the status Planned.
- **Related:** US-4.1, FR-003, FR-007, FR-008, FR-009, FR-010, FR-020

### SCR-4.3: Edit season page

- **Who can open it:** Owner only
- **Fields:** Name (required), Start date (required), End date (required)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - Show the current information of the season when the page opens.
  - The end date must be after the start date (FR-009).
  - Reject dates that overlap another season of the same league (FR-010).
  - If a game would be outside the new dates, do not save the change and show a message (FR-011).
  - When the owner clicks Save, show a confirm message before saving (FR-020).
- **Related:** US-4.2, FR-004, FR-009, FR-010, FR-011, FR-020

### SCR-4.4: View season page

- **Who can open it:** Owner only
- **Content:** Season information (League, Name, Start date, End date, Status) and a summary with three numbers: Total games, Games played, Games left
- **Buttons and links:** Edit, Change status, Close season, Reopen season, Delete, Back to list
- **Rules:**
  - Show the summary numbers (FR-016). For example, 30 games with 12 played shows 30 total, 12 played and 18 left.
  - Show Close season only when the status is not Completed.
  - Show Reopen season only when the status is Completed.
  - A Completed season is locked. Managers cannot change its results (FR-013).
- **Related:** US-4.4, US-4.5, US-4.6, US-4.7, FR-013, FR-016

### SCR-4.5: Change status page

- **Who can open it:** Owner only
- **Fields:** Status (choose Planned, In Progress or Completed)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - Show the current status when the page opens.
  - Choosing Completed locks the season. Show a short warning that managers will not be able to change results (FR-013).
  - After saving, show the new status on the season page.
  - When the owner clicks Save, show a confirm message before saving (FR-020).
- **Related:** US-4.5, US-4.6, FR-012, FR-013, FR-020

### SCR-4.6: Reopen season confirm message

- **Who can open it:** Owner only (shown after the owner clicks Reopen season)
- **Content:** The season name and a question such as "Do you want to reopen this season?"
- **Buttons and links:** Confirm reopen, Cancel
- **Rules:**
  - Only the owner can reopen a season. A manager is rejected (FR-013).
  - After reopen, the season status changes and results can be changed again.
- **Related:** US-4.7, FR-013

### SCR-4.7: Delete confirm message

- **Who can open it:** Owner only (shown after the owner clicks Delete)
- **Content:** The season name and a question such as "Do you want to delete this season?"
- **Buttons and links:** Confirm delete, Cancel
- **Rules:**
  - If the season has games, reject the delete and show a message. The season and its games stay unchanged (FR-014).
  - If the season has no games, change the record state to Deleted (soft delete). Do not remove the data (FR-015).
- **Related:** US-4.3, FR-005, FR-014, FR-015

### SCR-4.8: Confirm save message

- **Who can open it:** Owner only (shown after the owner clicks Save on SCR-4.2, SCR-4.3 or SCR-4.5)
- **Content:** A short question such as "Do you want to save this change?"
- **Buttons and links:** Confirm, Cancel
- **Rules:**
  - Nothing is saved until the owner clicks Confirm (FR-020).
  - Cancel returns the owner to the form with the information still filled in.
- **Related:** FR-020

### SCR-4.9: Public season list (on the league page)

- **Who can open it:** Everyone (no login needed)
- **Content:** The seasons of the league. Each season shows its name, dates and status.
- **Buttons and links:** Open a season
- **Rules:**
  - Show the current season first, then the past seasons (US-4.8).
  - Past seasons stay in the list with their games and results (FR-017).
  - Do not show any edit buttons.
  - Do not ask for login.
- **Related:** US-4.8, FR-017

### SCR-4.10: Public season page

- **Who can open it:** Everyone (no login needed)
- **Content:** The season name, dates, status, and its games and results
- **Buttons and links:** Back to league
- **Rules:**
  - Do not show any edit buttons.
  - Do not show a season with the state Deleted.
- **Related:** US-4.8, FR-017

### Rules for all screens

- Every screen MUST work on an office computer and on a phone (FR-019).
- Only the owner can change information. Other roles MUST be rejected (FR-018).
- Error messages MUST be short and clear.

-----

## Key Entities

- **Season** — A period when a league plays its games, for example Fall 2026.

-----

## Initial Data Model

### Season

- season_id: String — Required, unique
- league_id: String — Required
- name: String — Required
- start_date: Date — Required
- end_date: Date — Required, after start date
- status: String — Required (Planned, In Progress, Completed)
- record_state: String — Required (Active, Inactive, Deleted). Deleted is a soft delete, see shared/GLOSSARY.md

-----

## Gherkin AC

### US-4.1 — Add season

#### Scenario: Season is saved

- **Given** a season does not already exist
- **When** the owner enters the required season information and saves
- **Then** the system saves the season with the status Planned

#### Scenario: Season is not saved due to missing information

- **Given** a season is being added
- **When** required season information is missing
- **Then** the system does not save the season

#### Scenario: End date before start date is rejected

- **Given** a season is being added
- **When** the end date is before the start date
- **Then** the system does not save the season

#### Scenario: Overlapping season is rejected

- **Given** "Fall 2026" runs from Oct 1 to Dec 10 in "Fall League"
- **When** the owner adds a season from Nov 15 to Jan 20 in the same league
- **Then** the system rejects the season

#### Scenario: Wrong role cannot change information

- **Given** a manager is signed in
- **When** the manager tries to change information in this feature
- **Then** the system rejects the change

#### Scenario: Confirm before saving

- **Given** the user changes information
- **When** the user clicks save
- **Then** the system asks the user to confirm

### US-4.2 — Edit season dates

#### Scenario: Season is edited successfully

- **Given** a season exists
- **When** the owner changes the season information and saves
- **Then** the system saves the updated season

#### Scenario: Dates would cut off games

- **Given** "Fall 2026" has a game on Dec 8
- **When** the owner changes the end date to Dec 1
- **Then** the system does not save the change

### US-4.3 — Delete season

#### Scenario: Season is deleted successfully

- **Given** a season exists and has no games
- **When** the owner deletes the season
- **Then** the system removes the season from active records

#### Scenario: Season with games cannot be deleted

- **Given** a season has games
- **When** the owner tries to delete it
- **Then** the system rejects the delete operation
- **And** the season and its games stay unchanged

#### Scenario: Delete unknown season fails

- **Given** the season does not exist
- **When** the owner tries to delete it
- **Then** the system rejects the delete operation

### US-4.4 — View season summary

#### Scenario: Season summary is displayed

- **Given** "Fall 2026" has 30 games and 12 have results
- **When** the owner opens the season
- **Then** the system shows 30 games, 12 played and 18 left

### US-4.5 — Change season status

#### Scenario: Season becomes In Progress

- **Given** a season is Planned
- **When** the owner sets it to In Progress
- **Then** the system shows the season as In Progress

### US-4.6 — Close season

#### Scenario: Closed season is locked

- **Given** a season is Completed
- **When** a manager tries to change a result in it
- **Then** the system rejects the change

### US-4.7 — Reopen season

#### Scenario: Owner reopens a season

- **Given** a season is Completed
- **When** the owner reopens it
- **Then** the season status changes and results can be changed

#### Scenario: Manager cannot reopen a season

- **Given** a manager is signed in
- **When** the manager tries to reopen a season
- **Then** the system rejects the action

### US-4.8 — Public views seasons

#### Scenario: Current season is first

- **Given** a league has a current and a past season
- **When** a person opens the league page
- **Then** the system shows the current season first

#### Scenario: Past season is kept

- **Given** "Fall 2025" has ended
- **When** a person opens the league page
- **Then** "Fall 2025" is still listed with its games and results
