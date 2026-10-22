# Feature: Email

**Feature ID:** 15  
**Branch pattern:** `feature/15-email`  
**Status:** Draft  
**Created:** 2026-10-21  
**Input:** Send emails to refs, managers and players about games and news.  
**Depends on:** [Feature 5-Maintain-Game](Feature-5-Maintain-Game.md), [Feature 6-Maintain-Team](Feature-6-Maintain-Team.md), [Feature 7-Maintain-Player](Feature-7-Maintain-Player.md), [Feature 9-Maintain-Ref](Feature-9-Maintain-Ref.md), [Feature 10-Maintain-User](Feature-10-Maintain-User.md)

------

## User Stories

### US-15.1: Email refs

**As an** owner  
**I want to** email refs about their upcoming games  
**So that** they show up on time.  
**Priority:** P1  
**Independent test:** Send a message to refs and verify that a ref gets the game details.  
**Acceptance Scenarios:** see ### US-15.1 under Gherkin AC

### US-15.2: Email managers

**As an** owner  
**I want to** email managers their team schedule  
**So that** they plan ahead.  
**Priority:** P1  
**Independent test:** Send the schedule to managers and verify the content.  
**Acceptance Scenarios:** see ### US-15.2 under Gherkin AC

### US-15.3: Email players

**As an** owner  
**I want to** email players about upcoming games or any news  
**So that** they know when and where to play.  
**Priority:** P1  
**Independent test:** Send a message to one team and verify that only its players get it.  
**Acceptance Scenarios:** see ### US-15.3 under Gherkin AC

### US-15.4: Manager emails own team

**As a** manager  
**I want to** email only the players of my own team  
**So that** I can send reminders without asking the owner.  
**Priority:** P2  
**Independent test:** Send a message as a manager and verify the recipients.  
**Acceptance Scenarios:** see ### US-15.4 under Gherkin AC

### US-15.5: Use templates and free messages

**As an** owner  
**I want to** use ready templates or write a free message  
**So that** I save time and can send any news.  
**Priority:** P2  
**Independent test:** Choose a template and verify that the game details are filled in.  
**Acceptance Scenarios:** see ### US-15.5 under Gherkin AC

### US-15.6: Preview before sending

**As an** owner  
**I want to** see a preview and the number of people before I send  
**So that** I avoid mistakes.  
**Priority:** P1  
**Independent test:** Write a message and verify that the preview shows the number of people.  
**Acceptance Scenarios:** see ### US-15.6 under Gherkin AC

### US-15.7: Automatic game reminder

**As a** ref, manager or player  
**I want to** get a reminder 24 hours before my game  
**So that** I do not forget.  
**Priority:** P1  
**Independent test:** Set a game for tomorrow and verify that the reminder is sent.  
**Acceptance Scenarios:** see ### US-15.7 under Gherkin AC

### US-15.8: Game change notification

**As a** ref, manager or player  
**I want to** get an email at once when a game is moved, cancelled or changes location  
**So that** I do not go to the wrong place.  
**Priority:** P1  
**Independent test:** Move a game and verify that everyone gets an email.  
**Acceptance Scenarios:** see ### US-15.8 under Gherkin AC

### US-15.9: Ref assignment email

**As a** ref  
**I want to** get an email when I am assigned to a game, with a link to confirm or decline  
**So that** I can answer fast.  
**Priority:** P2  
**Independent test:** Assign a ref and verify that the email has the link.  
**Acceptance Scenarios:** see ### US-15.9 under Gherkin AC

### US-15.10: See email history and failures

**As an** owner  
**I want to** see the history of sent emails and the list of failed ones  
**So that** I know who did not get the message.  
**Priority:** P2  
**Independent test:** Open the history and verify that failed emails are listed.  
**Acceptance Scenarios:** see ### US-15.10 under Gherkin AC

### US-15.11: Turn off reminder emails

**As a** player  
**I want to** turn off reminder emails but still get game changes  
**So that** I am not annoyed by reminders.  
**Priority:** P3  
**Independent test:** Turn off reminders and verify that game changes still arrive.  
**Acceptance Scenarios:** see ### US-15.11 under Gherkin AC

-----

## Functional Requirements

- **FR-001:** The system MUST let the owner send an email to refs, managers or players, and to everyone in a group, one league or one team.
- **FR-002:** The system MUST let a manager send an email only to the players of their own team.
- **FR-003:** The system MUST have message templates (game reminder, schedule, cancelled game, ref assignment) that fill in the game details (date, time, location, teams).
- **FR-004:** The system MUST let the owner write a free message about anything.
- **FR-005:** The system MUST show a preview and the number of people before sending.
- **FR-006:** The system MUST check that each person has a valid email before sending.
- **FR-007:** The system MUST send a reminder 24 hours before each game. The owner MUST be able to turn the reminders on or off.
- **FR-008:** The system MUST NOT send the same reminder twice to the same person for the same game.
- **FR-009:** The system MUST email the managers, the players and the refs at once when a game is moved, cancelled or changes location.
- **FR-010:** The system MUST send a ref an assignment email with a link to confirm or decline the game.
- **FR-011:** The system MUST let a player turn off reminder emails. Game change emails MUST always be sent.
- **FR-012:** Every reminder email MUST have a link to turn off reminders, because players do not have an account.
- **FR-013:** The system MUST keep a history of sent emails (date, group, subject, number sent) and the list of failed emails.
- **FR-014:** The system MUST let the owner and the managers use this feature (main user: owner), and MUST NOT let refs or the public send emails.
- **FR-015:** The system MUST work on an office computer and on a phone.

-----

## Key Entities

- **Email message** — A message sent to one or more people.
- **Message template** — A ready message that fills in the game details.
- **Email history** — The record of sent and failed emails.

-----

## Initial Data Model

### Email message

- message_id: String — Required, unique
- sender_user_id: String — Required
- recipient_group: String — Required (Refs, Managers, Players, Team, League, Everyone)
- subject: String — Required
- body: String — Required
- sent_at: DateTime — Required

### Email history

- history_id: String — Required, unique
- message_id: String — Required
- recipient_email: String — Required
- status: String — Required (Sent, Failed)
- failure_reason: String — Optional

### Email settings

- reminders_on: Boolean — Required
- reminder_hours_before: Integer — Required, 24

### Player email preference

- player_id: String — Required, unique
- reminders_on: Boolean — Required

-----

## Gherkin AC

### US-15.1 — Email refs

#### Scenario: Refs get their games

- **Given** Paul is a ref with 2 games this week
- **When** the owner sends "Upcoming games" to refs
- **Then** Paul gets an email with the date, time and location of his 2 games

#### Scenario: Wrong role cannot email all refs

- **Given** a ref is signed in
- **When** the ref tries to email all refs
- **Then** the system rejects the action

### US-15.2 — Email managers

#### Scenario: Managers get the schedule

- **Given** a schedule is published
- **When** the owner sends the schedule to managers
- **Then** each manager gets an email with the games of their team

### US-15.3 — Email players

#### Scenario: Only one team gets the message

- **Given** the owner chooses the team "Eagles"
- **When** the owner sends a message
- **Then** only the "Eagles" players get it

#### Scenario: Missing email is listed

- **Given** a player has no email
- **When** the owner sends a message to the team
- **Then** the system lists that player as not sent

### US-15.4 — Manager emails own team

#### Scenario: Manager can choose only own team

- **Given** a manager of "Eagles" is signed in
- **When** the manager sends a message
- **Then** the manager can choose only the "Eagles" players

### US-15.5 — Use templates and free messages

#### Scenario: Template fills the game details

- **Given** a game is at "Field 2" at 6 PM
- **When** the owner chooses the game reminder template
- **Then** the message shows the date, time, location and teams

#### Scenario: Free message is sent

- **Given** the owner writes a free message
- **When** the owner sends it
- **Then** the recipients get the message

### US-15.6 — Preview before sending

#### Scenario: Preview is displayed

- **Given** the owner wrote a message for all refs
- **When** the owner clicks preview
- **Then** the system shows the message and the number of people who will get it

### US-15.7 — Automatic game reminder

#### Scenario: Reminder is sent

- **Given** reminders are on and a game is tomorrow at 6 PM
- **When** it is 6 PM today
- **Then** the players, managers and refs get a reminder

#### Scenario: Reminders are turned off

- **Given** the owner turned reminders off
- **When** it is 24 hours before a game
- **Then** the system sends no reminder

#### Scenario: Reminder is not sent twice

- **Given** a reminder was already sent for a game
- **When** the system checks reminders again
- **Then** the person does not get a second reminder for that game

### US-15.8 — Game change notification

#### Scenario: Game is moved

- **Given** a game is at "Field 1" at 6 PM
- **When** the owner moves it to "Field 2" at 7 PM
- **Then** both managers, the players and the refs get an email with the new place and time

#### Scenario: Game is cancelled

- **Given** a game is scheduled
- **When** the owner cancels it with the reason "Rain"
- **Then** everyone in the game gets an email with the reason

### US-15.9 — Ref assignment email

#### Scenario: Assignment email is sent

- **Given** the owner assigns Paul to a game
- **When** the assignment is saved
- **Then** Paul gets an email with the game details and a confirm or decline link

### US-15.10 — See email history and failures

#### Scenario: History is displayed

- **Given** the owner sent a message to 10 people and 1 email failed
- **When** the owner opens the history
- **Then** the system shows 9 sent and 1 failed with the failed address

### US-15.11 — Turn off reminder emails

#### Scenario: Game change still arrives

- **Given** John turned off reminder emails
- **When** a game of John's team is cancelled
- **Then** John gets the cancel email

#### Scenario: Turn off with the email link

- **Given** John got a reminder email
- **When** John clicks the link to turn off reminders
- **Then** John gets no more reminders and still gets game change emails

#### Scenario: Reminder is not sent

- **Given** John turned off reminder emails
- **When** it is 24 hours before his game
- **Then** John does not get a reminder
