# Feature: Supplier Order Form Maintenance

**Feature ID:** 7
**Branch pattern:** `feature/7-supplier-order-form-maintenance`
**Status:** Draft
**Created:** 2026-09-25
**Input:** Maintain forms used to order products from suppliers.
**Depends on:** [Feature 4 — Item Maintenance](feature-4-item-maintenance.md); [Feature 5 — Supplier Maintenance](feature-5-supplier-maintenance.md)

---
## User Stories

### US-7.1: Add supplier order form
**As an** office employee
**I want to** add a supplier order form
**So that** supplier order information can be maintained.
**Priority:** P1
**Independent test:** Add a supplier order form and verify that it is saved.
**Acceptance Scenarios:** see US-7.1 under Gherkin AC

### US-7.2: Edit supplier order form
**As an** office employee
**I want to** edit a supplier order form
**So that** the order information stays accurate.
**Priority:** P1
**Independent test:** Edit a supplier order form and verify that the change is saved.
**Acceptance Scenarios:** see US-7.2 under Gherkin AC

### US-7.3: Delete supplier order form
**As an** office employee
**I want to** delete a supplier order form
**So that** incorrect forms can be removed.
**Priority:** P1
**Independent test:** Delete a supplier order form and verify that it is no longer active.
**Acceptance Scenarios:** see US-7.3 under Gherkin AC

### US-7.4: View supplier order form
**As an** office employee
**I want to** view a supplier order form
**So that** I can review the supplier order.
**Priority:** P1
**Independent test:** Open a supplier order form and verify the current information is displayed.
**Acceptance Scenarios:** see US-7.4 under Gherkin AC

---
## Functional Requirements

- **FR-001:** The system MUST maintain supplier order forms.
- **FR-002:** Each supplier order form MUST have a unique order identifier.
- **FR-003:** A supplier order form MUST identify the supplier.
- **FR-004:** A supplier order form MUST contain the items being ordered.
- **FR-005:** A supplier order form MUST contain quantity ordered for each item.
- **FR-006:** The system MUST allow authorized users to add, edit, delete, and view supplier order forms.
- **FR-007:** Quantity ordered MUST be greater than zero.
- **FR-008:** The system MUST reject duplicate supplier order identifiers.

---
## Key Entities

- **Supplier Order Form** — Information used to place an order with a supplier.
- **Supplier** — Supplier receiving the order.
- **Item** — Product being ordered.

---
## Initial Data Model

### Supplier Order Form

| Field             | Type               | Rules                       |
| ----------------- | ------------------ | ---------------------------- |
| supplier_order_id | String             | Required; unique            |
| supplier_id       | Supplier reference | Required                    |
| order_date        | Date                | Required                    |
| status            | String/Enum        | Draft, Ordered, Received    |
| items             | Item references    | Required                    |
| quantity_ordered  | Integer            | Required; greater than zero |

---
## Gherkin AC

### US-7.1 — Add supplier order form

#### Scenario: Supplier order form is saved successfully
- **Given** a supplier and at least one item exist
- **When** the employee enters the required order information and saves
- **Then** the system saves the supplier order form

#### Scenario: Missing supplier is rejected
- **Given** no supplier is selected
- **When** the employee tries to save the supplier order form
- **Then** the system does not save the supplier order form

#### Scenario: Missing item is rejected
- **Given** no item is added to the order
- **When** the employee tries to save the supplier order form
- **Then** the system does not save the supplier order form

#### Scenario: Invalid quantity is rejected
- **Given** the employee enters a quantity ordered of zero or less
- **When** the employee tries to save the supplier order form
- **Then** the system rejects the invalid quantity

#### Scenario: Duplicate supplier order ID is rejected
- **Given** a supplier order form with the same identifier already exists
- **When** the employee tries to add another supplier order form with that identifier
- **Then** the system rejects the duplicate supplier order form

### US-7.2 — Edit supplier order form

#### Scenario: Supplier order form is edited successfully
- **Given** a supplier order form exists
- **When** the employee changes order information and saves
- **Then** the system saves the updated supplier order form

#### Scenario: Supplier order form edit fails
- **Given** a supplier order form exists
- **When** required information is removed during edit
- **Then** the system does not save the update

### US-7.3 — Delete supplier order form

#### Scenario: Supplier order form is deleted successfully
- **Given** a supplier order form exists
- **When** the employee deletes the supplier order form
- **Then** the system removes the supplier order form from active records

#### Scenario: Delete unknown supplier order form fails
- **Given** the supplier order form does not exist
- **When** the employee tries to delete it
- **Then** the system rejects the delete operation

### US-7.4 — View supplier order form

#### Scenario: Supplier order form is displayed
- **Given** a supplier order form exists
- **When** the employee views the supplier order form
- **Then** the system displays the order information
