# Feature: User-Authentication and  Management
**Feature ID:** 1
**Branch pattern:** `feature/1-user-authentication-management`
**Status:** Draft
**Created:** 2026-09-10
**Input:** This feature lets church staff log in, lets administrators manage user accounts, and lets staff plan each service: what the service will cover and who will preach.
**Depends on:** [Feature-2 member management](<Feature-2 member management.md>) (only to choose the preacher from the member list)

---

## User Stories

### US-1.1: Log in
**As a** church staff user
**I want to** log in with my username and password
**So that** only approved people can use the church system.
**Priority:** P1
**Independent test:** A user with the right username and password logs in; a wrong password is rejected.
**Acceptance scenarios:** see ### US-1.1 under Gherkin AC

### US-1.2: Stay logged in during a session
**As a** logged-in user
**I want to** stay logged in while I work
**So that** I do not have to log in again for every action, and my account stays safe if I leave it.
**Priority:** P1
**Independent test:** The user stays logged in while active, and must log in again after being inactive for too long.
**Acceptance scenarios:** see ### US-1.2 under Gherkin AC

### US-1.3: Log out
**As a** logged-in user
**I want to** log out
**So that** no one else can use my account on a shared device.
**Priority:** P1
**Independent test:** After logging out, the user cannot open protected pages without logging in again.
**Acceptance scenarios:** see ### US-1.3 under Gherkin AC

### US-1.4: Create a user account
**As a** church administrator
**I want to** create an account for a staff member
**So that** they can log in and use the system.
**Priority:** P1
**Independent test:** The administrator creates an account, and the new user can log in with it.
**Acceptance scenarios:** see ### US-1.4 under Gherkin AC

### US-1.5: View user accounts
**As a** church administrator
**I want to** see the list of user accounts
**So that** I know who can use the system.
**Priority:** P1
**Independent test:** The administrator opens the list and sees each username and role, but no passwords.
**Acceptance scenarios:** see ### US-1.5 under Gherkin AC

### US-1.6: Edit a user account
**As a** church administrator
**I want to** change a user's details and reset their password
**So that** accounts stay correct and users who forget their password can log in again.
**Priority:** P1
**Independent test:** The administrator changes a user's role or password, and the change works at the next login.
**Acceptance scenarios:** see ### US-1.6 under Gherkin AC

### US-1.7: Delete a user account
**As a** church administrator
**I want to** delete a user account
**So that** people who should not have access cannot log in.
**Priority:** P1
**Independent test:** After the account is deleted, that user cannot log in.
**Acceptance scenarios:** see ### US-1.7 under Gherkin AC

### US-1.8: See today's service after login
**As a** logged-in user
**I want to** see today's service on the home page
**So that** I can quickly check the topic and who will preach.
**Priority:** P1
**Independent test:** After login, the home page shows today's service name, topic and preacher; if there is no service today, it shows a button to create one.
**Acceptance scenarios:** see ### US-1.8 under Gherkin AC

### US-1.9: Create a service
**As a** logged-in user
**I want to** create a service with a name and a date
**So that** the church has a plan for each meeting.
**Priority:** P1
**Independent test:** The user creates a service and it appears in the list of services.
**Acceptance scenarios:** see ### US-1.9 under Gherkin AC

### US-1.10: Set what the service will cover
**As a** logged-in user
**I want to** write the topic and the plan (agenda) of a service
**So that** everyone knows what the service will cover.
**Priority:** P1
**Independent test:** The user saves a topic and an agenda, and both show on the service page.
**Acceptance scenarios:** see ### US-1.10 under Gherkin AC

### US-1.11: Choose who will preach
**As a** logged-in user
**I want to** choose a church member as the preacher of a service
**So that** the preacher is clear before the service starts.
**Priority:** P1
**Independent test:** The user selects a member as preacher and the member's name shows on the service page.
**Acceptance scenarios:** see ### US-1.11 under Gherkin AC

### US-1.12: Edit or delete a service
**As a** logged-in user
**I want to** change or delete a service
**So that** the plan stays correct when things change.
**Priority:** P1
**Independent test:** The user changes the preacher of a service and the new name shows on the service page.
**Acceptance scenarios:** see ### US-1.12 under Gherkin AC

--------

## Functional Requirements

- **FR-001**: System MUST let a user log in with a valid username and password.
- **FR-002**: System MUST reject a wrong username or password and MUST NOT say which one was wrong.
- **FR-003**: System MUST create a session when a user logs in.
- **FR-004**: System MUST NOT let a user open protected pages without a valid session.
- **FR-005**: System MUST end the session when the user logs out.
- **FR-006**: System MUST end the session after a period of inactivity.
- **FR-007**: System MUST let an administrator create a user account with a username, a password and a role.
- **FR-008**: System MUST NOT allow two accounts with the same username.
- **FR-009**: System MUST store passwords in a hashed form, never as plain text.
- **FR-010**: System MUST let an administrator see the list of user accounts without showing passwords.
- **FR-011**: System MUST let an administrator edit a user's details and reset their password.
- **FR-012**: System MUST let an administrator delete a user account and MUST ask for confirmation first.
- **FR-013**: System MUST end all active sessions of an account when the account is deleted.
- **FR-014**: System MUST allow only administrators to create, view, edit and delete user accounts.
- **FR-015**: System MUST show today's service (name, topic and preacher) on the home page after login.
- **FR-016**: System MUST let a logged-in user create a service with a name and a date.
- **FR-017**: System MUST NOT save a service without a name and a date.
- **FR-018**: System MUST let a logged-in user write a topic and an agenda for a service.
- **FR-019**: System MUST let a logged-in user choose the preacher from the list of church members.
- **FR-020**: System MUST show the topic, agenda and preacher on the service page.
- **FR-021**: System MUST let a logged-in user edit a service.
- **FR-022**: System MUST let a logged-in user delete a service and MUST ask for confirmation first.

-----

## Initial Data Model

The system keeps three kinds of information.

- **Users:** username (required, must be different for each user), password (saved in a hashed form, never as plain text), role (administrator or staff), and the date the account was created.
- **Sessions:** which user is logged in, a unique session code, when the session started, and when it ends.
- **Services:** name (for example "Sunday service"), date, topic (optional), agenda (optional), the preacher (one church member, optional), and which user created the service. Other features, like attendance and rides, also use services.

-----

## Gherkin AC

### US-1.1 — Log in

#### Scenario: Successful login
* **Given** the user has a valid account
* **When** the user enters the correct username and password
* **Then** the system logs the user in
* **And** the system opens the home page

#### Scenario: Wrong username or password
* **Given** the user is on the login page
* **When** the user enters a wrong username or password
* **Then** the system does not log the user in
* **And** the system shows a general "invalid username or password" message

#### Scenario: Open a protected page without login
* **Given** the user is not logged in
* **When** the user tries to open a protected page
* **Then** the system sends the user to the login page

### US-1.2 — Stay logged in during a session

#### Scenario: Session stays active
* **Given** the user is logged in
* **When** the user keeps using the system within the allowed time
* **Then** the system keeps the session active

#### Scenario: Session ends after inactivity
* **Given** the user is logged in
* **When** the user is inactive for longer than the allowed time
* **Then** the system ends the session
* **And** the system asks the user to log in again

### US-1.3 — Log out

#### Scenario: Successful logout
* **Given** the user is logged in
* **When** the user chooses to log out
* **Then** the system ends the session
* **And** the system sends the user to the login page

#### Scenario: Protected page after logout
* **Given** the user has logged out
* **When** the user tries to open a protected page
* **Then** the system sends the user to the login page

### US-1.4 — Create a user account

#### Scenario: Successfully create an account
* **Given** the administrator is creating a new account
* **When** the administrator enters a new username, a password and a role, and saves
* **Then** the system creates the account
* **And** the new user can log in

#### Scenario: Username already used
* **Given** an account with a username already exists
* **When** the administrator creates another account with the same username
* **Then** the system does not create the account
* **And** the system tells the administrator that the username is already used

#### Scenario: Missing information
* **Given** the administrator is creating a new account
* **When** the administrator saves without a username or password
* **Then** the system does not create the account
* **And** the system shows which information is missing

### US-1.5 — View user accounts

#### Scenario: View the user list
* **Given** the administrator is logged in
* **When** the administrator opens the user accounts page
* **Then** the system shows each username and role
* **And** the system does not show any password

#### Scenario: A non-administrator cannot see accounts
* **Given** a staff user who is not an administrator is logged in
* **When** the user tries to open the user accounts page
* **Then** the system denies access

### US-1.6 — Edit a user account

#### Scenario: Change a user's role
* **Given** the administrator is viewing a user account
* **When** the administrator changes the role and saves
* **Then** the system saves the change

#### Scenario: Reset a password
* **Given** the administrator is viewing a user account
* **When** the administrator sets a new password and saves
* **Then** the user can log in with the new password
* **And** the old password no longer works

### US-1.7 — Delete a user account

#### Scenario: Successfully delete an account
* **Given** the administrator is viewing a user account
* **When** the administrator chooses to delete and confirms
* **Then** the system removes the account
* **And** the system ends all active sessions of that account
* **And** that user cannot log in again

#### Scenario: Cancel the deletion
* **Given** the administrator is asked to confirm the deletion
* **When** the administrator cancels
* **Then** the system keeps the account as it is

### US-1.8 — See today's service after login

#### Scenario: Show today's service
* **Given** a service is planned for today
* **When** the user logs in
* **Then** the home page shows the service name, topic and preacher

#### Scenario: No service today
* **Given** no service is planned for today
* **When** the user logs in
* **Then** the home page shows a message that there is no service today
* **And** the home page shows a button to create a service

### US-1.9 — Create a service

#### Scenario: Successfully create a service
* **Given** the user is creating a service
* **When** the user enters a name and a date and saves
* **Then** the system creates the service
* **And** the service appears in the list of services

#### Scenario: Missing name or date
* **Given** the user is creating a service
* **When** the user saves without a name or a date
* **Then** the system does not create the service
* **And** the system shows which information is missing

### US-1.10 — Set what the service will cover

#### Scenario: Save the topic and agenda
* **Given** the user is viewing a service
* **When** the user writes a topic and an agenda and saves
* **Then** the system saves them
* **And** the service page shows the topic and the agenda

### US-1.11 — Choose who will preach

#### Scenario: Choose a preacher
* **Given** the user is viewing a service and church members exist
* **When** the user selects a member as preacher and saves
* **Then** the service page shows the member's name as the preacher
* **And** today's service on the home page shows the same name

#### Scenario: No members yet
* **Given** no church members exist
* **When** the user tries to choose a preacher
* **Then** the system shows a message to add a member first

### US-1.12 — Edit or delete a service

#### Scenario: Change the preacher
* **Given** a service already has a preacher
* **When** the user selects a different member and saves
* **Then** the service page shows the new preacher

#### Scenario: Delete a service
* **Given** the user is viewing a service
* **When** the user chooses to delete and confirms
* **Then** the system removes the service
* **And** the service no longer appears in the list of services

#### Scenario: Cancel the deletion
* **Given** the user is asked to confirm the deletion of a service
* **When** the user cancels
* **Then** the system keeps the service as it is
