# Feature: User Authentication and Management

**Feature ID:** 1
**Branch pattern:** `feature/1-user-authentication-management`
**Status:** Draft
**Created:** 2026-09-10
**Input:** Church staff can log in. Admins manage user accounts. Staff plan each service: the topic and who will preach.
**Depends on:** [Feature-2 member management](<Feature-2 member management.md>)

---

## User Stories

### US-1.1: Log in
**As a** staff user
**I want to** log in with my username and password
**So that** only allowed people can use the system.

**Priority:** P1
**Independent test:** A user logs in with the right password. A wrong password does not work.
**Acceptance scenarios:** see ### US-1.1 under Gherkin AC

### US-1.2: Stay logged in
**As a** logged-in user
**I want to** stay logged in while I work
**So that** I do not need to log in again and again.

**Priority:** P1
**Independent test:** The user stays logged in while using the system and must log in again after a long break.
**Acceptance scenarios:** see ### US-1.2 under Gherkin AC

### US-1.3: Log out
**As a** logged-in user
**I want to** log out
**So that** no one else can use my account.

**Priority:** P1
**Independent test:** After logout, the user cannot open the pages without logging in.
**Aceptance scenarios:** see ### US-1.3 under Gherkin AC

### US-1.4: Create a user account
**As a** admin
**I want to** create an account for a staff member
**So that** they can log in.

**Priority:** P1
**Independent test:** The admin creates an account and the new user can log in.
**Acceptance scenarios:** see ### US-1.4 under Gherkin AC

### US-1.5: See user accounts
**As a** admin
**I want to** see the list of user accounts
**So that** I know who can use the system.

**Priority:** P2
**Independent test:** The admin sees usernames and roles, but no passwords.
**Acceptance scenarios:** see ### US-1.5 under Gherkin AC

### US-1.6: Edit a user account
**As a** admin
**I want to** change a user's details and reset a password
**So that** accounts stay correct and users can get back in.

**Priority:** P2
**Independent test:** The admin changes a role or a password and it works at the next login.
**Acceptance scenarios:** see ### US-1.6 under Gherkin AC

### US-1.7: Delete a user account
**As a** admin
**I want to** delete a user account
**So that** people who should not have access cannot log in.

**Priority:** P2
**Independent test:** After the account is deleted, the user cannot log in.
**Acceptance scenarios:** see ### US-1.7 under Gherkin AC

### US-1.8: See today's service
**As a** logged-in user
**I want to** see today's service on the home page
**So that** I can quickly see the topic and who will preach.

**Priority:** P1
**Independent test:** After login, the home page shows today's service. If there is none, it shows a button to create one.
**Acceptance scenarios:** see ### US-1.8 under Gherkin AC

### US-1.9: Create a service
**As a** logged-in user
**I want to** create a service with a name and a date
**So that** the church has a plan for each meeting.

**Priority:** P1
**Independent test:** The user creates a service and it shows in the list of services.
**Acceptance scenarios:** see ### US-1.9 under Gherkin AC

### US-1.10: Set what the service will cover
**As a** logged-in user
**I want to** write the topic and the plan of a service
**So that** everyone knows what the service will cover.

**Priority:** P1
**Independent test:** The user saves a topic and a plan, and they show on the service page.
**Acceptance scenarios:** see ### US-1.10 under Gherkin AC

### US-1.11: Choose who will preach
**As a** logged-in user
**I want to** choose a church member as the preacher
**So that** everyone knows who will preach.

**Priority:** P1
**Independent test:** The user picks a member and the name shows on the service page.
**Acceptance scenarios:** see ### US-1.11 under Gherkin AC

### US-1.12: Edit or delete a service
**As a** logged-in user
**I want to** change or delete a service
**So that** the plan stays correct.

**Priority:** P2
**Independent test:** The user changes the preacher and the new name shows on the service page.
**Acceptance scenarios:** see ### US-1.12 under Gherkin AC

---

## Functional Requirements

- **FR-001**: System MUST let a user log in with a username and a password.
- **FR-002**: System MUST NOT log in a user with a wrong username or password, and MUST show a general message.
- **FR-003**: System MUST create a session when a user logs in.
- **FR-004**: System MUST NOT let a user open pages without logging in.
- **FR-005**: System MUST end the session when the user logs out.
- **FR-006**: System MUST end the session after a long time of no use.
- **FR-007**: System MUST let an admin create a user account with a username, a password and a role.
- **FR-008**: System MUST NOT allow two accounts with the same username.
- **FR-009**: System MUST save passwords in a hashed form, not as plain text.
- **FR-010**: System MUST let an admin see the list of accounts, without passwords.
- **FR-011**: System MUST let an admin edit an account and reset a password.
- **FR-012**: System MUST let an admin delete an account, after a confirmation.
- **FR-013**: System MUST end the sessions of an account when the account is deleted.
- **FR-014**: System MUST allow only admins to manage user accounts.
- **FR-015**: System MUST show today's service (name, topic and preacher) on the home page after login.
- **FR-016**: System MUST let a logged-in user create a service with a name and a date.
- **FR-017**: System MUST NOT save a service without a name and a date.
- **FR-018**: System MUST let a logged-in user write a topic and a plan for a service.
- **FR-019**: System MUST let a logged-in user choose the preacher from the member list.
- **FR-020**: System MUST let a logged-in user edit a service.
- **FR-021**: System MUST let a logged-in user delete a service, after a confirmation.

---

## Initial Data Model

The system keeps three things:

- **Users:** username (must be different for each user), password (saved in a hashed form), role (admin or staff), and the date the account was created.
- **Sessions:** which user is logged in, a session code, the start time, and the end time.
- **Services:** name, date, topic (optional), plan (optional), the preacher (one member, optional), and who created it. Other features also use services.

---

## Gherkin AC

### US-1.1 — Log in

#### Scenario: Successful login
* **Given** the user has an account
* **When** the user enters the right username and password
* **Then** the system logs the user in
* **And** the home page opens

#### Scenario: Wrong password
* **Given** the user is on the login page
* **When** the user enters a wrong username or password
* **Then** the system does not log the user in
* **And** the system shows "wrong username or password"

#### Scenario: Page without login
* **Given** the user is not logged in
* **When** the user tries to open a page
* **Then** the system shows the login page

### US-1.2 — Stay logged in

#### Scenario: Stay logged in
* **Given** the user is logged in
* **When** the user keeps using the system
* **Then** the session stays active

#### Scenario: Session ends
* **Given** the user is logged in
* **When** the user does nothing for a long time
* **Then** the system ends the session
* **And** the system asks the user to log in again

### US-1.3 — Log out

#### Scenario: Log out
* **Given** the user is logged in
* **When** the user clicks log out
* **Then** the system ends the session
* **And** the login page opens

#### Scenario: Page after logout
* **Given** the user logged out
* **When** the user tries to open a page
* **Then** the system shows the login page

### US-1.4 — Create a user account

#### Scenario: Create an account
* **Given** the admin is creating an account
* **When** the admin enters a new username, a password and a role, and saves
* **Then** the system creates the account
* **And** the new user can log in

#### Scenario: Username already used
* **Given** an account with the username already exists
* **When** the admin creates another account with the same username
* **Then** the system does not create it
* **And** the system says the username is already used

### US-1.5 — See user accounts

#### Scenario: See the list
* **Given** the admin is logged in
* **When** the admin opens the user accounts page
* **Then** the system shows each username and role
* **And** the system does not show any password

#### Scenario: Staff user cannot see it
* **Given** a staff user is logged in
* **When** the user tries to open the user accounts page
* **Then** the system does not allow it

### US-1.6 — Edit a user account

#### Scenario: Change a role
* **Given** the admin is looking at an account
* **When** the admin changes the role and saves
* **Then** the system saves the change

#### Scenario: Reset a password
* **Given** the admin is looking at an account
* **When** the admin sets a new password and saves
* **Then** the user can log in with the new password
* **And** the old password does not work

### US-1.7 — Delete a user account

#### Scenario: Delete an account
* **Given** the admin is looking at an account
* **When** the admin clicks delete and confirms
* **Then** the system deletes the account
* **And** the user cannot log in again

#### Scenario: Cancel the delete
* **Given** the admin is asked to confirm
* **When** the admin clicks cancel
* **Then** the account stays the same

### US-1.8 — See today's service

#### Scenario: Service today
* **Given** a service is planned for today
* **When** the user logs in
* **Then** the home page shows the service name, topic and preacher

#### Scenario: No service today
* **Given** there is no service today
* **When** the user logs in
* **Then** the home page says there is no service today
* **And** the home page shows a button to create one

### US-1.9 — Create a service

#### Scenario: Create a service
* **Given** the user is creating a service
* **When** the user enters a name and a date and saves
* **Then** the system creates the service
* **And** it shows in the list of services

#### Scenario: Name or date missing
* **Given** the user is creating a service
* **When** the user saves without a name or a date
* **Then** the system does not create the service
* **And** the system shows what is missing

### US-1.10 — Set what the service will cover

#### Scenario: Save the topic and plan
* **Given** the user is looking at a service
* **When** the user writes a topic and a plan and saves
* **Then** the service page shows the topic and the plan

### US-1.11 — Choose who will preach

#### Scenario: Choose a preacher
* **Given** the user is looking at a service and members exist
* **When** the user picks a member as preacher and saves
* **Then** the service page shows the member's name as preacher
* **And** the home page shows the same name for today's service

#### Scenario: No members yet
* **Given** there are no members
* **When** the user tries to choose a preacher
* **Then** the system says to add a member first

### US-1.12 — Edit or delete a service

#### Scenario: Change the preacher
* **Given** a service has a preacher
* **When** the user picks a different member and saves
* **Then** the service page shows the new preacher

#### Scenario: Delete a service
* **Given** the user is looking at a service
* **When** the user clicks delete and confirms
* **Then** the system deletes the service
* **And** it is not in the list of services anymore

#### Scenario: Cancel the delete
* **Given** the user is asked to confirm
* **When** the user clicks cancel
* **Then** the service stays the same
