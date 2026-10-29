# Feature: Maintain Location

**Feature ID:** 8  
**Branch pattern:** `feature/8-maintain-location`  
**Status:** Draft  
**Created:** 2026-10-21  
**Input:** Maintain the places (fields, courts, gyms) where games are played.  
**Depends on:** [Feature 1-User-Authentication](Feature-1-User-Authentication.md)

------

## User Stories

### US-8.1: Add location

**As an** owner  
**I want to** add a location  
**So that** games have a place.  
**Priority:** P1  
**Independent test:** Add a location and verify that it is saved.  
**Acceptance Scenarios:** see ### US-8.1 under Gherkin AC

### US-8.2: Edit location

**As an** owner  
**I want to** edit a location  
**So that** the address and notes stay accurate.  
**Priority:** P1  
**Independent test:** Edit a location and verify that the change is saved.  
**Acceptance Scenarios:** see ### US-8.2 under Gherkin AC

### US-8.3: Delete location

**As an** owner  
**I want to** delete a location  
**So that** a location made by mistake can be removed.  
**Priority:** P1  
**Independent test:** Delete a location and verify that it is no longer active.  
**Acceptance Scenarios:** see ### US-8.3 under Gherkin AC

### US-8.4: View location

**As a** person from the public  
**I want to** see the name, address and a map link of a game location  
**So that** I can find the place easily.  
**Priority:** P2  
**Independent test:** Open a game page and verify that the address and map link are shown.  
**Acceptance Scenarios:** see ### US-8.4 under Gherkin AC

### US-8.5: Add fields to a location

**As an** owner  
**I want to** add several fields or courts to one location  
**So that** more than one game can happen there at the same time.  
**Priority:** P1  
**Independent test:** Add two fields and verify that both can be used at 6 PM.  
**Acceptance Scenarios:** see ### US-8.5 under Gherkin AC

### US-8.6: Block dates for a location

**As an** owner  
**I want to** block dates for a location  
**So that** no game is placed there when it cannot be used.  
**Priority:** P2  
**Independent test:** Block a date and verify that games cannot be placed there.  
**Acceptance Scenarios:** see ### US-8.6 under Gherkin AC

### US-8.7: See games at a location

**As an** owner  
**I want to** see the games at a location on a date  
**So that** I can plan the day.  
**Priority:** P3  
**Independent test:** Open a location day view and verify the games are listed.  
**Acceptance Scenarios:** see ### US-8.7 under Gherkin AC

### US-8.8: Make location inactive

**As an** owner  
**I want to** make a location inactive when it is closed  
**So that** it is not used for new games.  
**Priority:** P2  
**Independent test:** Make a location inactive and verify that it cannot be chosen.  
**Acceptance Scenarios:** see ### US-8.8 under Gherkin AC

-----

## Functional Requirements

- **FR-001:** The system MUST maintain locations.
- **FR-002:** Each location MUST have a unique identifier.
- **FR-003:** The system MUST allow authorized users to add locations.
- **FR-004:** The system MUST allow authorized users to edit locations.
- **FR-005:** The system MUST allow authorized users to delete locations.
- **FR-006:** The system MUST allow authorized users to view locations.
- **FR-007:** Required location information MUST be provided before the location can be saved (name, address).
- **FR-008:** A location MUST be able to have several fields or courts, and a game MUST be placed at one field.
- **FR-009:** The system MUST NOT put two games at the same field at the same time.
- **FR-010:** The system MUST let the owner block dates for a location, and MUST list the games already placed there on those dates.
- **FR-011:** The system MUST NOT use a blocked date or an Inactive location for a new game.
- **FR-012:** The system MUST warn the owner when a location with future games is made inactive.
- **FR-013:** The system MUST NOT delete a location that is used by games or teams.
- **FR-014:** Deleting a location MUST be a soft delete (record state Deleted), so other features keep the original location information.
- **FR-015:** The system MUST show the owner the games at a location on a date.
- **FR-016:** The public game page MUST show the address and a map link.
- **FR-017:** The system MUST let the owner use this feature (main user: owner), and MUST NOT let other roles change its information.
- **FR-018:** The system MUST work on an office computer and on a phone.
- **FR-019:** This feature is not used very often, so the system MUST ask the user to confirm before saving a change.

-----

## Screen Requirements

### SCR-8.1: Location list page

- **Who can open it:** Owner only
- **Content:** A table of locations with these columns: Name, Address, Number of fields, Record state
- **Buttons and links:** Add location, View, Edit, Delete, Make inactive / Make active
- **Rules:**
  - Locations with the state Deleted are not shown in the list.
  - Other roles cannot open this page (FR-017).
- **Related:** US-8.8, FR-006, FR-017

### SCR-8.2: Add location page

- **Who can open it:** Owner only
- **Fields:** Name (required), Address (required), Notes (optional, for example parking or entrance)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - If a required field is empty, do not save and show which field is missing (FR-007).
  - When the owner clicks Save, show a confirm message before saving (FR-019).
  - A new location starts with the state Active.
  - After saving, the owner can add fields to the location (SCR-8.5).
- **Related:** US-8.1, FR-003, FR-007, FR-019

### SCR-8.3: Edit location page

- **Who can open it:** Owner only
- **Fields:** Name (required), Address (required), Notes (optional), Record state (Active or Inactive)
- **Buttons and links:** Save, Cancel
- **Rules:**
  - Show the current information of the location when the page opens.
  - If a required field is removed, do not save the change (FR-007).
  - When the owner changes the state to Inactive and the location has future games, show SCR-8.9 (FR-012).
  - When the owner clicks Save, show a confirm message before saving (FR-019).
- **Related:** US-8.2, US-8.8, FR-004, FR-007, FR-012, FR-019

### SCR-8.4: View location page

- **Who can open it:** Owner only
- **Content:** Location information (Name, Address, Notes, Record state), the list of fields, and the list of blocked dates
- **Buttons and links:** Edit, Manage fields, Block dates, See games by date, Delete, Back to list
- **Rules:**
  - Show the information as read only.
- **Related:** US-8.5, US-8.6, US-8.7, FR-006

### SCR-8.5: Manage fields page

- **Who can open it:** Owner only
- **Content:** The list of fields or courts of the location
- **Fields:** Field name (required, for example Field 1)
- **Buttons and links:** Add field, Back to location
- **Rules:**
  - A location can have several fields or courts (FR-008).
  - Two games can be placed at the same time on different fields of the same location.
  - Two games cannot be placed at the same field at the same time (FR-009).
  - When the owner clicks Add field, show a confirm message before saving (FR-019).
- **Related:** US-8.5, FR-008, FR-009, FR-019

### SCR-8.6: Block dates page

- **Who can open it:** Owner only
- **Content:** The list of blocked dates of the location, and the games already placed at the location on the chosen date
- **Fields:** Date (required), Reason (optional)
- **Buttons and links:** Block date, Back to location
- **Rules:**
  - If games are already placed at the location on that date, list them so the owner can move them (FR-010).
  - A blocked date cannot be used for a new game (FR-011).
  - When the owner clicks Block date, show a confirm message before saving (FR-019).
- **Related:** US-8.6, FR-010, FR-011, FR-019

### SCR-8.7: Games at a location page

- **Who can open it:** Owner only
- **Fields:** Date (required)
- **Content:** The games at the location on that date, in time order. Each game shows time, teams and status.
- **Buttons and links:** Back to location
- **Rules:**
  - Show the games in time order (FR-015).
  - If there are no games, show "No games on this date".
- **Related:** US-8.7, FR-015

### SCR-8.8: Delete confirm message

- **Who can open it:** Owner only (shown after the owner clicks Delete)
- **Content:** The location name and a question such as "Do you want to delete this location?"
- **Buttons and links:** Confirm delete, Cancel
- **Rules:**
  - If the location is used by games or teams, reject the delete and show a message. The location and its games stay unchanged (FR-013).
  - If the location is not used, change the record state to Deleted (soft delete). Do not remove the data (FR-014).
  - Past games keep showing the original location information (FR-014).
- **Related:** US-8.3, FR-005, FR-013, FR-014

### SCR-8.9: Inactive location warning message

- **Who can open it:** Owner only (shown when the owner makes a location inactive and the location has future games)
- **Content:** A warning with the number of future games at the location, and a request to move them
- **Buttons and links:** Make inactive, Open the games of this location, Back
- **Rules:**
  - Show this message only when the location has future games (FR-012).
  - An inactive location cannot be used for a new game (FR-011).
- **Related:** US-8.8, FR-011, FR-012

### SCR-8.10: Confirm save message

- **Who can open it:** Owner only (shown after the owner clicks Save, Add field or Block date)
- **Content:** A short question such as "Do you want to save this change?"
- **Buttons and links:** Confirm, Cancel
- **Rules:**
  - Nothing is saved until the owner clicks Confirm (FR-019).
  - Cancel returns the owner to the form with the information still filled in.
- **Related:** FR-019

### SCR-8.11: Public location information (on the game page)

- **Who can open it:** Everyone (no login needed)
- **Content:** The location name, the address and a map link, shown on the public game page
- **Buttons and links:** Open map
- **Rules:**
  - The public game page must show the address and a map link (FR-016).
  - Do not show any edit buttons.
  - Do not ask for login.
- **Related:** US-8.4, FR-016

### Rules for all screens

- Every screen MUST work on an office computer and on a phone (FR-018).
- Only the owner can change information. Other roles MUST be rejected (FR-017).
- Error messages MUST be short and clear.

-----

## Key Entities

- **Location** — A place with one or more fields or courts where games are played.
- **Field** — One field, court or room inside a location.
- **Blocked date** — A date when a location cannot be used.

-----

## Initial Data Model

### Location

- location_id: String — Required, unique
- name: String — Required
- address: String — Required
- notes: String — Optional (parking, entrance)
- record_state: String — Required (Active, Inactive, Deleted). Deleted is a soft delete, see shared/GLOSSARY.md

### Field

- field_id: String — Required, unique
- location_id: String — Required
- name: String — Required (for example Field 1)

### Blocked date

- blocked_id: String — Required, unique
- location_id: String — Required
- blocked_date: Date — Required
- reason: String — Optional

-----

## Gherkin AC

### US-8.1 — Add location

#### Scenario: Location is saved

- **Given** a location does not already exist
- **When** the owner enters the required location information and saves
- **Then** the system saves the location

#### Scenario: Location is not saved due to missing information

- **Given** a location is being added
- **When** required location information is missing
- **Then** the system does not save the location

#### Scenario: Wrong role cannot change information

- **Given** a manager is signed in
- **When** the manager tries to change information in this feature
- **Then** the system rejects the change

#### Scenario: Confirm before saving

- **Given** the user changes information
- **When** the user clicks save
- **Then** the system asks the user to confirm

### US-8.2 — Edit location

#### Scenario: Location is edited successfully

- **Given** a location exists
- **When** the owner changes the location information and saves
- **Then** the system saves the updated location

#### Scenario: Location edit fails

- **Given** a location exists
- **When** required information is removed during edit
- **Then** the system does not save the update

### US-8.3 — Delete location

#### Scenario: Location is deleted successfully

- **Given** a location exists and is not used
- **When** the owner deletes the location
- **Then** the system removes the location from active records

#### Scenario: Location used by games cannot be deleted

- **Given** a location has games
- **When** the owner tries to delete it
- **Then** the system rejects the delete operation
- **And** the location and its games stay unchanged

#### Scenario: Deleted location does not change past records

- **Given** a location was deleted and past games refer to it
- **When** someone views those games
- **Then** the system still shows the original location information

#### Scenario: Delete unknown location fails

- **Given** the location does not exist
- **When** the owner tries to delete it
- **Then** the system rejects the delete operation

### US-8.4 — View location

#### Scenario: Public sees address and map link

- **Given** a game is at "City Park Field 2"
- **When** a person who is not logged in opens the game page
- **Then** the system shows the address and a map link

### US-8.5 — Add fields to a location

#### Scenario: Two fields at the same time

- **Given** "City Park" has "Field 1" and "Field 2"
- **When** two games are placed at 6 PM, one on each field
- **Then** the system accepts both games

#### Scenario: Same field at the same time is rejected

- **Given** "Field 1" has a game at 6 PM
- **When** the owner puts another game at "Field 1" at 6 PM
- **Then** the system rejects the second game

### US-8.6 — Block dates for a location

#### Scenario: Date is blocked

- **Given** "Field 2" is free on Nov 8
- **When** the owner blocks Nov 8 for "Field 2"
- **Then** the system saves the blocked date

#### Scenario: Blocked date lists games

- **Given** "Field 2" has 2 games on Nov 1
- **When** the owner blocks Nov 1 for "Field 2"
- **Then** the system lists those 2 games so the owner can move them

#### Scenario: Game cannot use a blocked date

- **Given** "Field 2" is blocked on Nov 8
- **When** the owner adds a game at "Field 2" on Nov 8
- **Then** the system rejects the game

### US-8.7 — See games at a location

#### Scenario: Games at a location are listed

- **Given** "Field 2" has 3 games on Nov 1
- **When** the owner opens "Field 2" for Nov 1
- **Then** the system lists the 3 games in time order

### US-8.8 — Make location inactive

#### Scenario: Inactive location cannot be chosen

- **Given** a location is Inactive
- **When** the owner adds a game at that location
- **Then** the system rejects the game

#### Scenario: Inactive location has future games

- **Given** "Field 2" has 2 future games
- **When** the owner makes the location inactive
- **Then** the system warns about the 2 games and asks the owner to move them
