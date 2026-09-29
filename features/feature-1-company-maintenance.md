# Feature: Company Maintenance

**Feature ID:** 1
**Branch pattern:** `feature/1-company-maintenance`
**Status:** Draft
**Created:** 2026-09-20
**Input:** Maintain company information for the Warehouse system.
**Depends on:** None

---

## User Stories

### US-1.1: Add company

**As a** company manager
**I want to** add company information
**So that** the company can be maintained in the system.
**Priority:** P1
**Independent test:** Add a company and verify that it is saved.
**Acceptance Scenarios:** see ### US-1.1 under Gherkin AC

### US-1.2: Edit company

**As a** company manager
**I want to** edit company information
**So that** company information stays accurate.
**Priority:** P1
**Independent test:** Edit company information and verify that the change is saved.
**Acceptance Scenarios:** see ###  US-1.2 under Gherkin AC

### US-1.3: Deactivate company

**As a** company manager
**I want to** deactivate company information
**So that** incorrect company information can be removed.
**Priority:** P1
**Independent test:** Delete a company and verify that it no longer exists.
**Acceptance Scenarios:** see ### US-1.3 under Gherkin AC

### US-1.4: View company

**As a** company manager
**I want to** view company information
**So that** I can see the current company information.
**Priority:** P1
**Independent test:** Open company information and verify the current information is displayed.
**Acceptance Scenarios:** see ### US-1.4 under Gherkin AC

---



## Functional Requirements

- **FR-001**: The system MUST maintain company information.
- **FR-002**: The system MUST allow an authorized user to add company information.
- **FR-003**: The system MUST allow an authorized user to edit company information.
- **FR-004**: The system MUST allow an authorized user to delete company information.
- **FR-005**: The system MUST allow an authorized user to view company information.
- **FR-006**: Required company information MUST be provided before the company can be saved.
- **FR-007**: The system MUST reject a company when required information is missing.

---



## Key Entities

- **Company**: The company operating the warehouse.

---



## Initial Data Model



### Company


| Field      | Type    | Rules            |
| ---------- | ------- | ---------------- |
| company_id | String  | Required; unique |
| name       | String  | Required         |
| address    | String  | Required         |
| phone      | String | Required         |
| email      | String  | Optional         |


---



## Gherkin AC



### US-1.1 — Add company



#### Scenario: Company is saved

- **Given** a company does not already exist
- **When** the manager enters the required company information and saves
- **Then** the system saves the company



#### Scenario: Company is not saved

- **Given** a company is being added
- **When** required company information is missing
- **Then** the system does not save the company



#### Scenario: Duplicate company is rejected

- **Given** the company already exists
- **When** the manager tries to add the same company identifier
- **Then** the system rejects the duplicate company

---



### US-1.2 — Edit company



#### Scenario: Company is edited

- **Given** a company exists
- **When** the manager changes company information and saves
- **Then** the system saves the updated company



#### Scenario: Company edit is not saved

- **Given** a company exists
- **When** required information is removed
- **Then** the system does not save the update

---



### US-1.3 — Deactivate company



#### Scenario: Company is deactivate

- **Given** a company exists
- **When** the manager deletes the company
- **Then** the system removes the company from active records



#### Scenario: Unknown company cannot be deactivate

- **Given** the company does not exist
- **When** the manager tries to delete it
- **Then** the system rejects the delete operation

---



### US-1.4 — View company



#### Scenario: Company information is displayed

- **Given** a company exists
- **When** the manager views the company
- **Then** the system displays the company information

