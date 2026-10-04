# Feature: Inventory Maintenance

**Feature ID:** 3  
**Branch pattern:** `feature/3-inventory-maintenance`  
**Status:** Draft  
**Created:** 2026-09-22
**Input:** Maintain the quantity of items in each warehouse.  
**Depends on:** [Feature 2 — Warehouse Maintenance](feature-2-warehouse-maintenance.md); [Feature 4 — Item Maintenance](feature-4-item-maintenance.md)

---
## User Stories

### US-3.1: Add inventory

**As a** warehouse employee
**I want to** add inventory for an item in a warehouse
**So that** the system knows how many items are available.
**Priority:** P1
**Independent test:** Add an inventory record and verify that it is saved.
**Acceptance Scenarios:** see ### US-3.1 under Gherkin AC

### US-3.2: Edit inventory

**As a** warehouse employee
**I want to** edit inventory quantity
**So that** inventory information stays accurate.
**Priority:** P1
**Independent test:** Edit an inventory quantity and verify that the change is saved.
**Acceptance Scenarios:** see ### US-3.2 under Gherkin AC

### US-3.3: Delete inventory

**As a** warehouse employee
**I want to** delete an inventory record
**So that** incorrect inventory records can be removed.
**Priority:** P1
**Independent test:** Delete an inventory record and verify that it is no longer active.
**Acceptance Scenarios:** see ### US-3.3 under Gherkin AC

### US-3.4: View inventory

**As a** warehouse employee
**I want to** view inventory
**So that** I can see how many items are in each warehouse.
**Priority:** P1
**Independent test:** Open inventory and verify the current quantity is displayed.
**Acceptance Scenarios:** see ### US-3.4 under Gherkin AC

---
## Functional Requirements

- **FR-001:** The system MUST maintain inventory quantities.
- **FR-002:** Inventory MUST identify the item.
- **FR-003:** Inventory MUST identify the warehouse.
- **FR-004:** Inventory MUST maintain quantity on hand.
- **FR-005:** Quantity on hand MUST NOT be negative.
- **FR-006:** The system MUST allow authorized users to add inventory.
- **FR-007:** The system MUST allow authorized users to edit inventory.
- **FR-008:** The system MUST allow authorized users to delete inventory.
- **FR-009:** The system MUST allow authorized users to view inventory.
- **FR-010:** An item and warehouse combination MUST identify one inventory record.

---


## Key Entities

- **Inventory** — Quantity of an item stored in a warehouse.
- **Item** — Product stored and sold by the warehouse.
- **Warehouse** — Physical location where the inventory is stored.


---

## Initial Data Model



### Inventory


| Field            | Type                | Rules                     |
| ---------------- | ------------------- | ------------------------- |
| inventory_id     | String              | Required; unique          |
| item_id          | Item reference      | Required                  |
| warehouse_id     | Warehouse reference | Required                  |
| quantity_on_hand | Integer             | Required; zero or greater |


---

## Gherkin AC



### US-3.1 — Add inventory



#### Scenario: Inventory is added successfully

- **Given** an item and a warehouse both exist
- **When** the employee enters a quantity on hand and saves
- **Then** the system saves the inventory record



#### Scenario: Inventory is rejected when item is missing

- **Given** no item is selected
- **When** the employee tries to save the inventory record
- **Then** the system does not save the inventory record



#### Scenario: Inventory is rejected when warehouse is missing

- **Given** no warehouse is selected
- **When** the employee tries to save the inventory record
- **Then** the system does not save the inventory record



#### Scenario: Negative quantity is rejected

- **Given** the employee enters a negative quantity on hand
- **When** the employee tries to save the inventory record
- **Then** the system rejects the negative quantity



#### Scenario: Duplicate item/warehouse inventory is rejected

- **Given** an inventory record already exists for an item and warehouse
- **When** the employee tries to add another inventory record for the same item and warehouse
- **Then** the system rejects the duplicate inventory record



### US-3.2 — Edit inventory



#### Scenario: Inventory is edited successfully

- **Given** an inventory record exists
- **When** the employee changes the quantity on hand and saves
- **Then** the system saves the updated inventory record



#### Scenario: Invalid edit is rejected

- **Given** an inventory record exists
- **When** the employee enters a negative quantity on hand and saves
- **Then** the system does not save the update



### US-3.3 — Delete inventory



#### Scenario: Inventory record is deleted successfully

- **Given** an inventory record exists
- **When** the employee deletes the inventory record
- **Then** the system removes the inventory record



#### Scenario: Delete unknown inventory record

- **Given** the inventory record does not exist
- **When** the employee tries to delete it
- **Then** the system rejects the delete operation



### US-3.4 — View inventory



#### Scenario: Inventory is displayed

- **Given** an inventory record exists
- **When** the employee views inventory
- **Then** the system displays the item, warehouse, and quantity on hand

