# Feature: User Authentication

**Feature ID:** 1  
**Branch pattern:** `feature/1-user-authentication`  
**Status:** Draft  
**Created:** 2026-10-19  
**Input:** Let owners, managers and refs log in and out of the Sports system safely.  
**Depends on:** None

---

## User Stories

### US-1.1: Log in

**As a** user  
**I want to** log in with my email and password  
**So that** I can use the pages for my role.  
**Priority:** P1  
**Independent test:** Log in with a correct account and verify that the home page for the role opens.  
**Acceptance Scenarios:** see ### US-1.1 under Gherkin AC

### US-1.2: Log out

**As a** user  
**I want to** log out when I want  
**So that** I can end my session safely.  
**Priority:** P1  
**Independent test:** Log out and verify that the pages need login again.  
**Acceptance Scenarios:** see ### US-1.2 under Gherkin AC

### US-1.3: Lock account after wrong passwords

**As a** user  
**I want to** have my account locked after 5 wrong passwords  
**So that** nobody can guess my password.  
**Priority:** P1  
**Independent test:** Enter 5 wrong passwords and verify that the account is locked.  
**Acceptance Scenarios:** see ### US-1.3 under Gherkin AC

### US-1.4: Unlock account

**As an** owner  
**I want to** unlock a locked account  
**So that** a real user is not blocked for a long time.  
**Priority:** P2  
**Independent test:** Unlock a locked account and verify that the user can log in.  
**Acceptance Scenarios:** see ### US-1.4 under Gherkin AC

### US-1.5: Change temporary password at first login

**As a** new user  
**I want to** change my temporary password at my first login  
**So that** only I know my password.  
**Priority:** P1  
**Independent test:** Log in with a temporary password and verify that a new password is required.  
**Acceptance Scenarios:** see ### US-1.5 under Gherkin AC

### US-1.6: Reset forgotten password

**As a** user  
**I want to** reset my password with a link sent to my email  
**So that** I can get back in when I forget it.  
**Priority:** P1  
**Independent test:** Request a reset, use the link, and verify that the new password works.  
**Acceptance Scenarios:** see ### US-1.6 under Gherkin AC

### US-1.7: Change my own password

**As a** user  
**I want to** change my password when I am logged in  
**So that** I can keep it fresh.  
**Priority:** P2  
**Independent test:** Change the password and verify that the new password works at the next login.  
**Acceptance Scenarios:** see ### US-1.7 under Gherkin AC

### US-1.8: Log out after no activity

**As a** user  
**I want to** be logged out after 30 minutes with no activity  
**So that** nobody can use my account on a shared computer.  
**Priority:** P2  
**Independent test:** Wait 30 minutes and verify that the next click needs login.  
**Acceptance Scenarios:** see ### US-1.8 under Gherkin AC

### US-1.9: See only my role's pages

**As a** user  
**I want to** see only the menu items my role can use  
**So that** I do not get confused and cannot open other pages.  
**Priority:** P1  
**Independent test:** Log in as each role and verify the menu.  
**Acceptance Scenarios:** see ### US-1.9 under Gherkin AC

### US-1.10: View public pages without login

**As a** person from the public  
**I want to** view the public pages without logging in  
**So that** I can follow games easily.  
**Priority:** P1  
**Independent test:** Open the public standings page without login and verify that it displays.  
**Acceptance Scenarios:** see ### US-1.10 under Gherkin AC

---



## Functional Requirements

- **FR-001:** The system MUST have a login page, and MUST NOT let anyone open owner, manager or ref pages without logging in.
- **FR-002:** The system MUST let a user log in with a unique email and a password.
- **FR-003:** The system MUST store passwords in a safe  form and MUST NOT store them as plain text.
- **FR-004:** The system MUST show the same message for a wrong email and a wrong password.
- **FR-005:** The system MUST lock an account for 15 minutes after 5 wrong passwords.
- **FR-006:** The system MUST let the owner unlock a locked account.
- **FR-007:** The system MUST make a new user change the temporary password at the first login.
- **FR-008:** The system MUST send a password reset link by email. The link MUST work only once and MUST expire after 1 hour.
- **FR-009:** The system MUST let a logged in user change their own password by entering the old password first.
- **FR-010:** The system MUST log a user out when the user clicks logout and after 30 minutes with no activity.
- **FR-011:** The system MUST show only the menu items allowed for the user's role (owner, manager or ref).
- **FR-012:** The system MUST send the user back to the page they wanted to open after login.
- **FR-013:** The system MUST NOT require login for the public pages.
- **FR-014:** Accounts are created by the owner. The system MUST NOT let people create their own account.
- **FR-015:** The first owner account MUST be created when the system is set up, not through the login page.
- **FR-016:** The system MUST work on a computer and on a phone.

---



## Key Entities

- **User account** — A person who can log in as owner, manager or ref.
- **Session** — One login of a user, from login until logout or timeout.
- **Password reset link** — A one time link sent by email to set a new password.

---



## Initial Data Model



### User account

- user_id: String — Required, unique
- email: String — Required, unique
- password_hash: String — Required
- role: String — Required (Owner, Manager, Ref)
- record_state: String — Required (Active, Inactive, Deleted). 
- must_change_password: Boolean — Required, true for a new user
- failed_login_count: Integer — Required
- locked_until: DateTime — Optional
- last_login: DateTime — Optional



### Session

- session_id: String — Required, unique
- user_id: String — Required
- started_at: DateTime — Required
- last_activity_at: DateTime — Required



### Password reset link

- token: String — Required, unique
- user_id: String — Required
- expires_at: DateTime — Required
- is_used: Boolean — Required

---



## Gherkin AC



### US-1.1 — Log in



#### Scenario: Login succeeds

- **Given** an active user account exists
- **When** the user enters the correct email and password
- **Then** the system opens the home page for the user's role



#### Scenario: Wrong password is rejected

- **Given** an active user account exists
- **When** the user enters a wrong password
- **Then** the system rejects the login
- **And** the message does not say which part was wrong



#### Scenario: Unknown email is rejected

- **Given** no account has the email
- **When** someone tries to log in with that email
- **Then** the system rejects the login
- **And** the message is the same as for a wrong password



#### Scenario: Inactive account cannot log in

- **Given** the owner made the account inactive
- **When** the user enters the correct email and password
- **Then** the system rejects the login



### US-1.2 — Log out



#### Scenario: Logout ends the session

- **Given** a user is logged in
- **When** the user clicks logout
- **Then** the system ends the session and shows the login page



### US-1.3 — Lock account after wrong passwords



#### Scenario: Account is locked

- **Given** a user entered 4 wrong passwords
- **When** the user enters a 5th wrong password
- **Then** the system locks the account for 15 minutes



#### Scenario: Locked account cannot log in

- **Given** an account is locked
- **When** the user enters the correct password
- **Then** the system rejects the login and shows that the account is locked



#### Scenario: Lock ends after 15 minutes

- **Given** an account was locked 15 minutes ago
- **When** the user enters the correct password
- **Then** the system opens the home page



### US-1.4 — Unlock account



#### Scenario: Owner unlocks an account

- **Given** a manager account is locked
- **When** the owner unlocks it
- **Then** the manager can log in again



#### Scenario: Other roles cannot unlock

- **Given** a manager is logged in
- **When** the manager tries to unlock an account
- **Then** the system rejects the action



### US-1.5 — Change temporary password at first login



#### Scenario: New password is required

- **Given** the owner created an account with a temporary password
- **When** the user logs in for the first time
- **Then** the system asks for a new password before the user can continue



#### Scenario: Weak password is rejected

- **Given** the user must set a new password
- **When** the user enters a password that is too short
- **Then** the system rejects the password



### US-1.6 — Reset forgotten password



#### Scenario: Reset link is sent

- **Given** an account exists
- **When** the user asks to reset the password
- **Then** the system sends a reset link to the user's email



#### Scenario: Reset link works only once

- **Given** the user already used a reset link
- **When** the user opens the same link again
- **Then** the system rejects the link



#### Scenario: Expired link is rejected

- **Given** a reset link is older than 1 hour
- **When** the user opens the link
- **Then** the system rejects the link



### US-1.7 — Change my own password



#### Scenario: Password is changed

- **Given** a user is logged in
- **When** the user enters the old password and a new password and saves
- **Then** the system saves the new password



#### Scenario: Wrong old password fails

- **Given** a user is logged in
- **When** the user enters a wrong old password
- **Then** the system does not change the password



### US-1.8 — Log out after no activity



#### Scenario: Idle user is logged out

- **Given** a user is logged in and does nothing for 30 minutes
- **When** the user clicks any page
- **Then** the system shows the login page



### US-1.9 — See only my role's pages



#### Scenario: Menu by role

- **Given** a ref is logged in
- **When** the ref looks at the menu
- **Then** the ref sees only the schedule and pay pages



#### Scenario: Page without login

- **Given** a person is not logged in
- **When** the person opens a manager page
- **Then** the system shows the login page



#### Scenario: Return to wanted page

- **Given** a person was sent to the login page from a page
- **When** the person logs in
- **Then** the system opens the page the person wanted



#### Scenario: Wrong role page is blocked

- **Given** a manager is logged in
- **When** the manager opens the user maintenance page
- **Then** the system rejects the request



### US-1.10 — View public pages without login



#### Scenario: Public page opens

- **Given** a person is not logged in
- **When** the person opens the public standings page
- **Then** the system displays the page



#### Scenario: Public cannot see edit buttons

- **Given** a person is not logged in
- **When** the person opens a public page
- **Then** the system shows no edit buttons

  ## Screen Requirements

### SCR-1.1: Login page

- **Who can open it:** Everyone (no login needed)
- **Fields:** Email, Password
- **Buttons and links:** Log in, Forgot password
- **Rules:**
  - Show the same error message for a wrong email and a wrong password.
  - If the account is locked, show a message that the account is locked and for how long.
  - After login, open the page the user wanted, or the home page of the role.
  - The password field hides the characters.
- **Related:** US-1.1, US-1.3, FR-001, FR-002

### SCR-1.2: Forgot password page

- **Who can open it:** Everyone (no login needed)
- **Fields:** Email
- **Buttons and links:** Send reset link, Back to login
- **Rules:**
  - After the user clicks send, show a message that a link was sent if the account exists.
  - The message is the same whether the email exists or not.
- **Related:** US-1.6, FR-008

### SCR-1.3: Reset password page

- **Who can open it:** A person with a valid reset link
- **Fields:** New password, Confirm new password
- **Buttons and links:** Save password
- **Rules:**
  - If the link is used or older than 1 hour, show an error and a link to the forgot password page.
  - Reject a password that is too short or does not match the confirm field.
  - After saving, send the user to the login page with a success message.
- **Related:** US-1.6, FR-008

### SCR-1.4: Change temporary password page

- **Who can open it:** A user with a temporary password, right after the first login
- **Fields:** New password, Confirm new password
- **Buttons and links:** Save password
- **Rules:**
  - The user cannot open any other page until the password is changed.
  - Reject a password that is too short or does not match the confirm field.
  - After saving, open the home page of the user's role.
- **Related:** US-1.5, FR-007

### SCR-1.5: Change my password page

- **Who can open it:** Any logged in user
- **Fields:** Old password, New password, Confirm new password
- **Buttons and links:** Save password, Cancel
- **Rules:**
  - The old password must be correct, or the password is not changed.
  - Reject a password that is too short or does not match the confirm field.
  - Show a success message after saving.
- **Related:** US-1.7, FR-009

### SCR-1.6: Home page and menu

- **Who can open it:** Any logged in user
- **Content:** A menu and a Log out button
- **Rules:**
  - Show only the menu items for the user's role: owner, manager or ref.
  - A ref sees only the schedule and pay pages.
  - If the user opens a page that the role cannot use, reject the request.
  - The Log out button ends the session and shows the login page.
  - After 30 minutes with no activity, the next click shows the login page.
- **Related:** US-1.2, US-1.8, US-1.9, FR-010, FR-011

### SCR-1.7: Unlock account (owner only)

- **Who can open it:** Owner only
- **Content:** A list of user accounts with their status (Active, Inactive, Locked)
- **Buttons and links:** Unlock (shown only for locked accounts)
- **Rules:**
  - Manager and ref users cannot open this screen (FR-006).
  - After unlock, the user can log in again and the failed password count goes back to 0.
- **Related:** US-1.4, FR-006

### SCR-1.8: Public pages (for example, public standings)

- **Who can open it:** Everyone (no login needed)
- **Rules:**
  - Do not ask for login (FR-013).
  - Do not show any edit buttons.
  - Show a link to the login page for staff.
- **Related:** US-1.10, FR-013

### Rules for all screens

- Every screen MUST work on a computer and on a phone (FR-016).
- Error messages MUST be short and clear, and MUST NOT show private details such as which part of the login was wrong.

