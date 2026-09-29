# Feature: Put Away Received Items
**Feature ID:** 11
**Branch pattern:** `feature/11-put-away-received-items`
**Status:** Draft
**Created:** 2026-09-25
**Input:** Put received products into a warehouse location.
**Depends on:** [Feature 10 — Receive Supplier Order](feature-10-receive-supplier-order.md); [Feature 2 — Warehouse Maintenance](feature-2-warehouse-maintenance.md)

---
## User Stories

### US-11.1: Put away received items
**As a** warehouse employee
**I want to** put received items into a warehouse location
**So that** items can be stored and found later.
**Priority:** P1
**Independent test:** Put away a received item and verify the put away record is saved.
**Acceptance Scenarios:** see ### US-11.1 under Gherkin AC

### US-11.2: Record storage location
**As a** warehouse employee
**I want to** record where items are stored
**So that** warehouse employees know where to find them.
**Priority:** P1
**Independent test:** Enter a storage location on a put away record and verify it is saved.
**Acceptance Scenarios:** see ### US-11.2 under Gherkin AC

### US-11.3: Edit storage location
**As a** warehouse employee
**I want to** change an item's storage location
**So that** the system reflects the current location.
**Priority:** P1
**Independent test:** Edit a storage location and verify the change is saved.
**Acceptance Scenarios:** see ### US-11.3 under Gherkin AC

### US-11.4: Remove storage location
**As a** warehouse employee
**I want to** remove an incorrect storage location
**So that** incorrect location information can be corrected.
**Priority:** P1
**Independent test:** Remove a storage location and verify it is no longer saved.
**Acceptance Scenarios:** see ### US-11.4 under Gherkin AC

---
## Functional Requirements

- **FR-001:** The system MUST allow received items to be assigned to a warehouse.
- **FR-002:** The system MUST maintain the storage location of received items.
- **FR-003:** A storage location MUST identify the warehouse.
- **FR-004:** The system MUST NOT allow an item to be put away without a warehouse location.
- **FR-005:** The system MUST update the item's inventory location when put away.

---
## Key Entities

- **Put Away Record** — Record of where a received item was stored.
- **Item** — Product being put away.
- **Warehouse** — Location where the item is stored.

---
## Initial Data Model

### Put Away Record

| Field         | Type                | Rules                        |
| -------------- | ------------------- | ------------------------------ |
| put_away_id   | String              | Required; unique             |
| item_id       | Item reference      | Required                     |
| warehouse_id  | Warehouse reference | Required                     |
| location      | String              | Required                     |
| quantity      | Integer             | Required; greater than zero  |
| put_away_date | Date                 | Required                     |

---
## Gherkin AC

### US-11.1 — Put away received items

#### Scenario: Successful put away
- **Given** received items exist for a supplier order
- **When** the employee puts the items away to a warehouse location
- **Then** the system saves the put away record

#### Scenario: Missing warehouse
- **Given** no warehouse is selected
- **When** the employee tries to put the items away
- **Then** the system does not save the put away record

### US-11.2 — Record storage location

#### Scenario: Missing location
- **Given** no storage location is entered
- **When** the employee tries to put the items away
- **Then** the system does not save the put away record

#### Scenario: Invalid quantity
- **Given** the employee enters a quantity of zero or less
- **When** the employee tries to save the put away record
- **Then** the system rejects the invalid quantity

### US-11.3 — Edit storage location

#### Scenario: Editing location
- **Given** a put away record exists
- **When** the employee changes the storage location and saves
- **Then** the system saves the updated storage location

### US-11.4 — Remove storage location

#### Scenario: Removing incorrect location
- **Given** a put away record has an incorrect storage location
- **When** the employee removes the storage location
- **Then** the system removes the storage location from the put away record
