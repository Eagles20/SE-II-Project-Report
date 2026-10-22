# Feature: Maintain Sport

**Feature ID:** 2  
**Branch pattern:** `feature/2-maintain-sport`  
**Status:** Draft  
**Created:** 2026-10-19  
**Input:** Maintain sports for the sports league system.  
**Depends on:** [Feature 1 — User-Authentication](feature-1-User-Authentication.md)       

------

## User Stories

### US-2.1: Add sport

**As an** owner  
**I want to** add a sport  
**So that** leagues can be created for it.  
**Priority:** P1  
**Independent test:** Add a sport and verify that it is saved.  
**Acceptance Scenarios:** see ### US-2.1 under Gherkin AC

### US-2.2: Edit sport

**As an** owner  
**I want to** edit a sport  
**So that** the sport information stays accurate.  
**Priority:** P1  
**Independent test:** Edit a sport and verify that the change is saved.  
**Acceptance Scenarios:** see ### US-2.2 under Gherkin AC

### US-2.3: Delete sport

**As an** owner  
**I want to** delete a sport  
**So that** a sport made by mistake or never used can be removed.  
**Priority:** P1  
**Independent test:** Delete a sport and verify that it is no longer active.  
**Acceptance Scenarios:** see ### US-2.3 under Gherkin AC

### US-2.4: View sport

**As an** owner  
**I want to** view sport information  
**So that** I can see the current sports and how many leagues each has.  
**Priority:** P1  
**Independent test:** Open the sport list and verify that the information is displayed.  
**Acceptance Scenarios:** see ### US-2.4 under Gherkin AC

### US-2.5: Make sport inactive

**As an** owner  
**I want to** make a sport inactive instead of deleting it  
**So that** old records stay but the sport is hidden from the public.  
**Priority:** P2  
**Independent test:** Make a sport inactive and verify that the public cannot see it.  
**Acceptance Scenarios:** see ### US-2.5 under Gherkin AC

### US-2.6: Search sports

**As an** owner  
**I want to** search sports by name  
**So that** I can find a sport fast.  
**Priority:** P3  
**Independent test:** Search for a sport name and verify that it is found.  
**Acceptance Scenarios:** see ### US-2.6 under Gherkin AC

### US-2.7: Public views sports

**As a** person from the public  
**I want to** see the active sports and their leagues  
**So that** I can find the league I care about.  
**Priority:** P2  
**Independent test:** Open the public sports page and verify that active sports are shown without edit buttons.  
**Acceptance Scenarios:** see ### US-2.7 under Gherkin AC

-----

## Functional Requirements

- **FR-001:** The system MUST maintain sports (for example flag football, softball, basketball, soccer).
- **FR-002:** Each sport MUST have a unique identifier.
- **FR-003:** The system MUST allow authorized users to add sports.
- **FR-004:** The system MUST allow authorized users to edit sports.
- **FR-005:** The system MUST allow authorized users to delete sports.
- **FR-006:** The system MUST allow authorized users to view sports.
- **FR-007:** Required sport information MUST be provided before the sport can be saved (name, gender group).
- **FR-008:** The system MUST reject a duplicate sport name. The check MUST NOT depend on capital letters.
- **FR-009:** The system MUST NOT delete a sport that has leagues.
- **FR-010:** Deleting a sport MUST be a soft delete (record state Deleted), so other features keep the original sport information.
- **FR-011:** A sport MUST have a record state (Active, Inactive or Deleted. Inactive sports MUST be hidden from the public but all data MUST stay.
- **FR-012:** The system MUST let the owner search sports by name and MUST show the number of leagues for each sport.
- **FR-013:** The system MUST let the owner use this feature (main user: owner), and MUST NOT let other roles change its information.
- **FR-014:** The system MUST work on an office computer and on a phone.
- **FR-015:** This feature is not used very often, so the system MUST ask the user to confirm before saving a change.

-----

## Key Entities

- **Sport** — A sport played in the league, for example Men's Basketball.

-----

## Initial Data Model

### Sport

- sport_id: String — Required, unique
- name: String — Required
- gender_group: String — Required (Men, Women, Co-ed)
- description: String — Optional
- record_state: String — Required (Active, Inactive, Deleted). Deleted is a soft delete, see shared/GLOSSARY.md

-----

## Gherkin AC

### US-2.1 — Add sport

#### Scenario: Sport is saved

- **Given** a sport does not already exist
- **When** the owner enters the required sport information and saves
- **Then** the system saves the sport

#### Scenario: Sport is not saved due to missing information

- **Given** a sport is being added
- **When** required sport information is missing
- **Then** the system does not save the sport

#### Scenario: Duplicate sport name is rejected

- **Given** a sport named "Soccer" exists
- **When** the owner adds a sport named "soccer" with the same gender group
- **Then** the system rejects the duplicate sport

#### Scenario: Men and Women versions are allowed

- **Given** Basketball for Men exists
- **When** the owner adds Basketball for Women
- **Then** the system saves it as a different sport

#### Scenario: Wrong role cannot change information

- **Given** a manager is signed in
- **When** the manager tries to change information in this feature
- **Then** the system rejects the change

#### Scenario: Confirm before saving

- **Given** the user changes information
- **When** the user clicks save
- **Then** the system asks the user to confirm

### US-2.2 — Edit sport

#### Scenario: Sport is edited successfully

- **Given** a sport exists
- **When** the owner changes the sport information and saves
- **Then** the system saves the updated sport

#### Scenario: Sport edit fails

- **Given** a sport exists
- **When** required information is removed during edit
- **Then** the system does not save the update

### US-2.3 — Delete sport

#### Scenario: Sport is deleted successfully

- **Given** a sport exists and has no leagues
- **When** the owner deletes the sport
- **Then** the system removes the sport from active records

#### Scenario: Sport with leagues cannot be deleted

- **Given** a sport has leagues
- **When** the owner tries to delete it
- **Then** the system rejects the delete operation
- **And** the sport and its leagues stay unchanged

#### Scenario: Deleted sport does not change past records

- **Given** a sport was deleted and past records refer to it
- **When** someone views those past records
- **Then** the system still shows the original sport information

#### Scenario: Delete unknown sport fails

- **Given** the sport does not exist
- **When** the owner tries to delete it
- **Then** the system rejects the delete operation

### US-2.4 — View sport

#### Scenario: Sport information is displayed

- **Given** a sport exists
- **When** the owner views the sport
- **Then** the system displays the sport information and its number of leagues

### US-2.5 — Make sport inactive

#### Scenario: Inactive sport is hidden

- **Given** a sport is made inactive
- **When** the public opens the sports page
- **Then** the sport is not shown
- **And** the leagues, games and stats of the sport stay in the system

#### Scenario: Sport is made active again

- **Given** a sport is inactive
- **When** the owner makes it active
- **Then** the public can see the sport again

### US-2.6 — Search sports

#### Scenario: Search finds a sport

- **Given** sports exist
- **When** the owner searches for part of a sport name
- **Then** the system shows the matching sports

#### Scenario: Search finds nothing

- **Given** sports exist
- **When** the owner searches for a name that does not exist
- **Then** the system shows that no sport was found

### US-2.7 — Public views sports

#### Scenario: Public sees active sports

- **Given** active sports exist
- **When** a person who is not logged in opens the sports page
- **Then** the system shows the active sports and no edit buttons

#### Scenario: Public sees leagues of a sport

- **Given** a sport has leagues
- **When** the person opens the sport
- **Then** the system shows the leagues of the sport
