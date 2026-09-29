# Feature: Item Maintenance
**Feature ID:** 4
**Branch pattern:** `feature/4-item-maintenance`
**Status:** Draft
**Created:** 2026-09-25
**Input:** Maintain individual item information.
**Depends on:** Feature 5 — Supplier Maintenance

---
## User Stories

### US-4.1: Add item
**As a** warehouse manager
**I want to** add an item
**So that** the warehouse can maintain products.
**Priority:** P1
**Independent test:** Add an item and verify that it is saved.
**Acceptance Scenarios:** see ### US-4.1 under Gherkin AC

### US-4.2: Edit item
**As a** warehouse manager
**I want to** edit an item
**So that** item information stays accurate.
**Priority:** P1
**Independent test:** Edit an item and verify that the change is saved.
**Acceptance Scenarios:** see ### US-4.2 under Gherkin AC

### US-4.3: Delete item
**As a** warehouse manager
**I want to** delete an item
**So that** incorrect items can be removed.
**Priority:** P1
**Independent test:** Delete an item and verify that it is no longer active.
**Acceptance Scenarios:** see ### US-4.3 under Gherkin AC

### US-4.4: View item
**As a** warehouse employee
**I want to** view item information
**So that** I can identify the product.
**Priority:** P1
**Independent test:** Open an item and verify the current information is displayed.
**Acceptance Scenarios:** see ### US-4.4 under Gherkin AC

---
## Functional Requirements

- **FR-001:** The system MUST maintain individual items.
- **FR-002:** Each item MUST have a unique SKU.
- **FR-003:** Each item MUST have a unique UPC when a UPC is provided.
- **FR-004:** The system MUST maintain price.
- **FR-005:** The system MUST maintain SKU.
- **FR-006:** The system MUST maintain UPC.
- **FR-007:** The system MUST maintain supplier.
- **FR-008:** The system MUST maintain description.
- **FR-009:** The system MUST allow authorized users to add, edit, delete, and view items.
- **FR-010:** The system MUST reject duplicate SKU values.
- **FR-011:** The system MUST reject duplicate UPC values.

---
## Key Entities

- **Item** — A product maintained by the warehouse.

---
## Initial Data Model
### Item
| Field       | Type               | Rules                     |
| ----------- | ------------------ | -------------------------- |
| item_id     | String             | Required; unique          |
| price       | Decimal            | Required; zero or greater |
| sku         | String             | Required; unique          |
| upc         | String             | Optional; unique          |
| supplier_id | Supplier reference | Required                  |
| description | String             | Required                  |

---
## Gherkin AC
### US-4.1 — Add item

#### Scenario: Item is saved successfully
- **Given** a supplier exists
- **When** the manager enters the required item information and saves
- **Then** the system saves the item
#### Scenario: Item is not saved due to missing information
- **Given** an item is being added
- **When** required item information is missing
- **Then** the system does not save the item
#### Scenario: Duplicate SKU is rejected
- **Given** an item with a SKU already exists
- **When** the manager tries to add another item with the same SKU
- **Then** the system rejects the duplicate SKU
#### Scenario: Duplicate UPC is rejected
- **Given** an item with a UPC already exists
- **When** the manager tries to add another item with the same UPC
- **Then** the system rejects the duplicate UPC

### US-4.2 — Edit item

#### Scenario: Item is edited successfully
- **Given** an item exists
- **When** the manager changes item information and saves
- **Then** the system saves the updated item

#### Scenario: Item edit fails
- **Given** an item exists
- **When** required information is removed during edit
- **Then** the system does not save the update

### US-4.3 — Delete item

#### Scenario: Item is deleted successfully
- **Given** an item exists
- **When** the manager deletes the item
- **Then** the system removes the item from active records

#### Scenario: Delete unknown item fails
- **Given** the item does not exist
- **When** the manager tries to delete it
- **Then** the system rejects the delete operation

### US-4.4 — View item

#### Scenario: Item information is displayed
- **Given** an item exists
- **When** the employee views the item
- **Then** the system displays the item information