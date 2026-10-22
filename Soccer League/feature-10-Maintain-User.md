# Feature: Maintain User

**Feature ID:** 10  
**Branch pattern:** `feature/10-maintain-user`  
**Status:** Draft  
**Created:** 2026-10-21  
**Input:** Maintain the accounts of owners, managers and refs.  
**Depends on:** [Feature 1-User-Authentication](Feature-1-User-Authentication.md)

------

## User Stories

### US-10.1: Add user

**As an** owner  
**I want to** create an account for a manager or a ref  
**So that** they can log in.  
**Priority:** P1  
**Independent test:** Create a user and verify that a temporary password email is sent.  
**Acceptance Scenarios:** see ### US-10.1 under Gherkin AC

### US-10.2: Edit user

**As an** owner  
**I want to** edit a user and change the role  
**So that** I can fix mistakes or move people.  
**Priority:** P1  
**Independent test:** Edit a user and verify that the change is saved.  
**Acceptance Scenarios:** see ### US-10.2 under Gherkin AC

### US-10.3: Make user inactive or active

**As an** owner  
**I want to** make a user inactive and make the user active again  
**So that** people who leave cannot log in but their history stays.  
**Priority:** P1  
**Independent test:** Make a user inactive and verify that the login is rejected.  
**Acceptance Scenarios:** see ### US-10.3 under Gherkin AC

### US-10.4: Delete user

**As an** owner  
**I want to** delete a user who never did anything in the system  
**So that** wrong accounts can be removed.  
**Priority:** P2  
**Independent test:** Delete an unused user and verify that the user is no longer active.  
**Acceptance Scenarios:** see ### US-10.4 under Gherkin AC

### US-10.5: View and search users

**As an** owner  
**I want to** filter users by role, search by name or email, and see the last login  
**So that** I can find people and see who is active.  
**Priority:** P2  
**Independent test:** Filter by role and verify that only those users are shown.  
**Acceptance Scenarios:** see ### US-10.5 under Gherkin AC

### US-10.6: Reset another user's password

**As an** owner  
**I want to** reset the password of another user  
**So that** I can help someone who is locked out.  
**Priority:** P2  
**Independent test:** Reset a password and verify that a temporary password is sent.  
**Acceptance Scenarios:** see ### US-10.6 under Gherkin AC

### US-10.7: Link manager to team and ref to ref record

**As an** owner  
**I want to** link a manager account to a team and a ref account to a ref record  
**So that** each person sees only their own data.  
**Priority:** P1  
**Independent test:** Link a manager to a team and verify that the manager sees only that team.  
**Acceptance Scenarios:** see ### US-10.7 under Gherkin AC

### US-10.8: Edit own profile

**As a** manager  
**I want to** edit my own name, phone and email  
**So that** my details stay right.  
**Priority:** P3  
**Independent test:** Edit own details and verify that the role cannot be changed.  
**Acceptance Scenarios:** see ### US-10.8 under Gherkin AC

-----

## Functional Requirements

- **FR-001:** The system MUST maintain users.
- **FR-002:** Each user MUST have a unique identifier.
- **FR-003:** The system MUST allow authorized users to add users.
- **FR-004:** The system MUST allow authorized users to edit users.
- **FR-005:** The system MUST allow authorized users to delete users.
- **FR-006:** The system MUST allow authorized users to view users.
- **FR-007:** Required user information MUST be provided before the user can be saved (name, email, role).
- **FR-008:** The system MUST reject a duplicate email.
- **FR-009:** The system MUST send a temporary password by email when the owner creates a user.
- **FR-010:** A manager user MUST be linked to a team, and a ref user MUST be linked to a ref record.
- **FR-011:** A user MUST have a record state (Active, Inactive or Deleted). An Inactive user MUST NOT be able to log in.
- **FR-012:** The system MUST NOT make inactive or delete the last active owner.
- **FR-013:** The system MUST NOT delete a user who did something in the system. The owner can make the user inactive instead.
- **FR-014:** Deleting a user MUST be a soft delete (record state Deleted), so other features keep the original user information.
- **FR-015:** The system MUST let the owner reset the password of another user.
- **FR-016:** The system MUST NOT change the role of a manager who is linked to a team, or of a ref who is linked to a ref record, until the link is removed.
- **FR-017:** The system MUST keep a history of changes to users (who, when, what), including role changes, making a user inactive, and password resets.
- **FR-018:** The system MUST let the owner filter users by role, search by name or email, and see the last login.
- **FR-019:** A manager or a ref MUST be able to edit their own name, phone and email, and MUST NOT be able to change their own role.
- **FR-020:** The system MUST let the owner use this feature (main user: owner), and MUST NOT let other roles change other users.
- **FR-021:** The system MUST work on an office computer and on a phone.
- **FR-022:** This feature is not used very often, so the system MUST ask the user to confirm before saving a change.

-----

## Key Entities

- **User** — A person with an account and a role (Owner, Manager or Ref).
- **User change history** — The record of who changed a user account and when.

-----

## Initial Data Model

### User

- user_id: String — Required, unique
- name: String — Required
- email: String — Required, unique
- phone: String — Optional
- role: String — Required (Owner, Manager, Ref)
- team_id: String — Required for a manager
- ref_id: String — Required for a ref
- last_login: DateTime — Optional
- record_state: String — Required (Active, Inactive, Deleted).

### User change history

- change_id: String — Required, unique
- user_id: String — Required
- action: String — Required (Role change, Made inactive, Made active, Password reset)
- changed_by: String — Required
- changed_at: DateTime — Required

-----

## Gherkin AC

### US-10.1 — Add user

#### Scenario: User is saved

- **Given** a user does not already exist
- **When** the owner enters the required user information and saves
- **Then** the system saves the user

#### Scenario: Temporary password is sent

- **Given** the owner creates a manager account
- **When** the user is saved
- **Then** the system sends an email with a temporary password

#### Scenario: User is not saved due to missing information

- **Given** a user is being added
- **When** required user information is missing
- **Then** the system does not save the user

#### Scenario: Duplicate email is rejected

- **Given** a user with the email sam@example.com exists
- **When** the owner adds another user with the same email
- **Then** the system rejects the duplicate user

#### Scenario: Wrong role cannot change information

- **Given** a manager is signed in
- **When** the manager tries to change another user
- **Then** the system rejects the change

#### Scenario: Confirm before saving

- **Given** the user changes information
- **When** the user clicks save
- **Then** the system asks the user to confirm

### US-10.2 — Edit user

#### Scenario: User is edited successfully

- **Given** a user exists
- **When** the owner changes the user information and saves
- **Then** the system saves the updated user

#### Scenario: User edit fails

- **Given** a user exists
- **When** required information is removed during edit
- **Then** the system does not save the update

#### Scenario: Role change is blocked while linked

- **Given** a manager is linked to "Eagles"
- **When** the owner changes the role to Ref
- **Then** the system rejects the change and asks to remove the link first

### US-10.3 — Make user inactive or active

#### Scenario: Inactive user cannot log in

- **Given** the owner made "Sam" inactive
- **When** Sam tries to log in
- **Then** the system rejects the login and shows that the account is inactive

#### Scenario: User is made active again

- **Given** a user is Inactive
- **When** the owner makes the user active
- **Then** the user can log in again

#### Scenario: Last owner is protected

- **Given** there is only one active owner
- **When** the owner tries to make that account inactive
- **Then** the system rejects the action

#### Scenario: Change is recorded

- **Given** the owner makes "Sam" inactive
- **When** the change is saved
- **Then** the history shows who did it and when

### US-10.4 — Delete user

#### Scenario: User is deleted successfully

- **Given** a user exists and did nothing in the system
- **When** the owner deletes the user
- **Then** the system removes the user from active records

#### Scenario: User with history cannot be deleted

- **Given** a user entered results
- **When** the owner tries to delete the user
- **Then** the system rejects the delete operation
- **And** the system suggests to make the user inactive

#### Scenario: Last owner cannot be deleted

- **Given** there is only one active owner
- **When** the owner tries to delete that account
- **Then** the system rejects the delete operation

#### Scenario: Delete unknown user fails

- **Given** the user does not exist
- **When** the owner tries to delete the user
- **Then** the system rejects the delete operation

### US-10.5 — View and search users

#### Scenario: Filter by role

- **Given** users with several roles exist
- **When** the owner filters by "Ref"
- **Then** the system shows only refs

#### Scenario: Last login is displayed

- **Given** a user logged in yesterday
- **When** the owner opens the user list
- **Then** the system shows the last login of the user

### US-10.6 — Reset another user's password

#### Scenario: Owner resets a password

- **Given** a user exists
- **When** the owner resets the password
- **Then** the system sends a temporary password and the user must change it at the next login

### US-10.7 — Link manager to team and ref to ref record

#### Scenario: Manager sees own team

- **Given** a manager is linked to "Eagles"
- **When** the manager logs in
- **Then** the manager sees only "Eagles"

#### Scenario: Manager without a team is rejected

- **Given** a manager account has no team
- **When** the owner saves the user
- **Then** the system does not save the user

### US-10.8 — Edit own profile

#### Scenario: Own profile is saved

- **Given** a manager is signed in
- **When** the manager changes the phone number and saves
- **Then** the system saves the new phone number

#### Scenario: Own role cannot be changed

- **Given** a manager is signed in
- **When** the manager tries to change their own role
- **Then** the system rejects the change
