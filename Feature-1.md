# Feature: User Authentication and Management
**Feature ID:** 1 
**Branch pattern:** `feature/1-user& authentication-management`  
**Status:** Draft  
**Created:** 2026-09-10  
**Input:** This feature lets church staff login, lets administrators manage user acconts, and lets staff plan each service: what service will cover and who will preach.
**Depends on:** None 

---

## User Stories

### US-N.1: Log in 
**As a** Church stuff user 
**I want to** log in with my username and password
**So that** only approved people can user the church system .

**Priority:** P1  
**Independent test:** A user with the right username and password logs in; a wrong password is rejected.  
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Stay logged in during a session
**As a**logged-in user 
**I want to**I Want to stay logged in while i work   
**So that** i do not have to log in again for every action, and my account stays safe if i leave it.

**Priority:** P1  
**Independent test:** The user stays logged in while active, and must log in again after being inactive for too long.  
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Log out
**As a** logged-in user
**I want to** log out
**So that** no one else can use my account on a shared device
**Priority:** P1
**Independent test:** After logging out, the user cannot open protected pages without logging in again.
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

### US-N.4: Create a user account
**As a** church administrator
**I want to** Create an account for staff member
**So that** they can log in and use the system
**Priority:** P1
**Independent test:** The administrator creates an account, and the new user can log in with it.
**Acceptance scenarios:** see ### US-N.4 under Acceptance Criteria


---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow an authorized church user to add a new member.
- **FR-002**: Users MUST be able to enter the required information for a member.
- **FR-003**: MUST NOT allow a member to be registered without the required information.
- **FR-004**: System Must NOT allow duplicate member records when the member already exists.
- **FR-005**: System MUST save the member's informtion after successfull registration.

---



## Data Model Requirements

### `table_name` table
| Field | Type | Rules |
|-------|------|-------|
| `id` | INTEGER PK | Auto-increment |
| `first_name` | VARCHAR | Required  |
| `last_name`  | VARCHAR  |Required  |
|`phone`       | VARCHAR  |Optional  |
|`email`       | VARCHAR  |Optional   |
|`address`     | VARCHAR  |Optional  |

---


## Acceptance Criteria

### US-N.1 — Register a new member

#### Scenario: Successfully register a new member
*   **Given** the church administrator is registering a new member
*   **When** the administrator enters all required member information and submits the registration
*   **Then** the system saves the new member
*   **And** the new member appears in the member records

#### Scenario: Required information is missing
*   **Given** the church administrator is registering a new member
*   **When** the administrator submits the registration without required information
*   **Then** the system does not create a member
*   **And** the system indicates the missing required information

### US-N.2 — Save member informstion

#### Scenario: Member information is saved
*   **Given** the administrator has entered valid member information
*   **When** the administrator saves the member
*   **Then** the system stores the member information
*   **And** the saved information can be viewed later

#### Scenario: Duplicate memeber
*   **Given** the member already exist in the system
*   **When** the administrator tries to register the same member again
*   **Then** the system does not create a duplicate record
*   **And** the system informs the administrator that the member already exists

### US-N.3 -Choose a Language

### Scenario: Use the system in Spanish

- **Given** the system is available in English
- **When** the member selects Spanish
- **Then** the system displays the available information in Spanish

### Scenario: Use the system in English
- **Given** the system is available in Spanish
- **When** the member selects English
- **Then** the system displays the available information in English
