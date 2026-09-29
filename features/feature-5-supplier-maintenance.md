# Feature: Supplier Maintenance

**Feature ID:** 5
**Branch pattern:** `feature/5-supplier-maintenance`
**Status:** Draft
**Created:** 2026-09-25
**Input:** Maintain supplier information.
**Depends on:** Feature 1 — Company Maintenance

---
## User Stories

### US-5.1: Add supplier
**As an** office employee
**I want to** add a supplier
**So that** the warehouse can maintain supplier information.
**Priority:** P1
**Independent test:** Add a supplier and verify that it is saved.
**Acceptance Scenarios:** see US-5.1 under Gherkin AC

### US-5.2: Edit supplier
**As an** office employee
**I want to** edit a supplier
**So that** supplier information stays accurate.
**Priority:** P1
**Independent test:** Edit a supplier and verify that the change is saved.
**Acceptance Scenarios:** see US-5.2 under Gherkin AC

### US-5.3: Delete supplier
**As an** office employee
**I want to** delete a supplier
**So that** incorrect supplier information can be removed.
**Priority:** P1
**Independent test:** Delete a supplier and verify that it is no longer active.
**Acceptance Scenarios:** see US-5.3 under Gherkin AC

### US-5.4: View supplier
**As an** office employee
**I want to** view supplier information
**So that** I can see supplier details.
**Priority:** P1
**Independent test:** Open a supplier and verify the current information is displayed.
**Acceptance Scenarios:** see US-5.4 under Gherkin AC

---
## Functional Requirements

- **FR-001:** The system MUST maintain suppliers.
- **FR-002:** Supplier name MUST be required.
- **FR-003:** Supplier address MUST be maintained.
- **FR-004:** Supplier phone number MUST be maintained.
- **FR-005:** Supplier email MUST be maintained.
- **FR-006:** Supplier supply number MUST be maintained.
- **FR-007:** Supplier warehouse number MUST be maintained.
- **FR-008:** The system MUST allow authorized users to add, edit, delete, and view suppliers.
- **FR-009:** Supplier identifier MUST be unique.

---
## Key Entities

- **Supplier** — A company that supplies products to the warehouse.

---
## Initial Data Model

### Supplier

| Field            | Type   | Rules             |
| ---------------- | ------ | ----------------- |
| supplier_id      | String | Required; unique  |
| name             | String | Required          |
| address          | String | Required          |
| phone            | String | Required          |
| email            | String | Optional          |
| supply_number    | String | Required          |
| warehouse_number | String | Required          |

---
## Gherkin AC

### US-5.1 — Add supplier

#### Scenario: Supplier is added successfully
- **Given** a supplier does not already exist
- **When** the employee enters the required supplier information and saves
- **Then** the system saves the supplier

#### Scenario: Supplier is not saved due to missing information
- **Given** a supplier is being added
- **When** required supplier information is missing
- **Then** the system does not save the supplier

#### Scenario: Duplicate supplier is rejected
- **Given** a supplier with the same identifier already exists
- **When** the employee tries to add a supplier with that identifier
- **Then** the system rejects the duplicate supplier

### US-5.2 — Edit supplier

#### Scenario: Supplier is edited successfully
- **Given** a supplier exists
- **When** the employee changes supplier information and saves
- **Then** the system saves the updated supplier

#### Scenario: Supplier edit fails
- **Given** a supplier exists
- **When** required information is removed during edit
- **Then** the system does not save the update

### US-5.3 — Delete supplier

#### Scenario: Supplier is deleted successfully
- **Given** a supplier exists
- **When** the employee deletes the supplier
- **Then** the system removes the supplier from active records

#### Scenario: Delete unknown supplier fails
- **Given** the supplier does not exist
- **When** the employee tries to delete it
- **Then** the system rejects the delete operation

### US-5.4 — View supplier

#### Scenario: Supplier information is displayed
- **Given** a supplier exists
- **When** the employee views the supplier
- **Then** the system displays the supplier information